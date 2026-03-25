```
tip: <to be assigned>
title: Native BN254 Precompiles via Rust FFI
author: Anish Narang (@anishnarang9)
discussions-to: https://github.com/tronprotocol/tips/issues/843
status: Draft
type: Standards Track
category: VM
created: 2026-03-25
```

## Summary

Replace TRON's Java-based BN254 elliptic curve precompiled contracts (`0x06`, `0x07`, `0x08`) with native Rust implementations reached through JNI. The proposal preserves the current precompile addresses and EIP-196/197-compatible interface while introducing a feature flag, `allowRustZkPrecompiles`, for safe rollout and rollback.

## Abstract

This proposal adds a native execution path for BN254 point addition, scalar multiplication, and pairing checks inside `java-tron`. The TVM continues to dispatch precompile calls at addresses `0x06`, `0x07`, and `0x08`, but when `allowRustZkPrecompiles` is enabled and the native library is available, execution is routed through `NativeZkBridge` into a Rust `cdylib` backed by `arkworks-rs`.

The Rust side performs decoding, subgroup validation, arithmetic, and pairing checks, then returns the same output format as the existing Java BN128 implementation. The Java path remains the fallback implementation when the flag is disabled or the native library cannot be loaded.

On a private-node benchmark built during implementation, the Rust path reduced a 2-pair pairing check from `61,010.5 us` to `1,927.7 us` and turned a pairing transaction that timed out on the Java path into one that completed successfully. A real `circom` and `snarkjs` Groth16 proof also verified successfully on the Rust-enabled private node.

## Motivation

TRON already exposes Ethereum-compatible BN128 precompiles, but the Java implementation of pairing is too slow for practical zero-knowledge verification workloads.

Measured private-node results:

| Operation | Java path | Rust path | Speedup |
|-----------|-----------|-----------|---------|
| ecAdd (`0x06`) | 60.7 us | 17.3 us | 3.5x |
| ecMul (`0x07`) | 64.0 us | 46.0 us | 1.4x |
| ecPairing (`0x08`, 2 pairs) | 61,010.5 us | 1,927.7 us | 31.6x |

The key protocol problem is pairing:

- Java pairing transaction result: `OUT_OF_TIME`
- Rust pairing transaction result: `SUCCESS`
- Java pairing transaction energy usage: `10,000,000`
- Rust pairing transaction energy usage: `116,385`

Using the measured 2-pair benchmark as an estimate, the pairing-heavy portion of a 4-pair Groth16 verifier is approximately `122.0 ms` on the Java path and `3.9 ms` on the Rust path. This estimate is an inference from measured 2-pair timing, not a direct 4-pair transaction benchmark.

Without a faster pairing path, TRON cannot support Groth16 verification, ZK rollups, shielded transfers, or proof-based bridge verification with comfortable runtime headroom.

## Specification

### Precompile Addresses

| Address | Operation | Input | Output |
|---------|-----------|-------|--------|
| `0x06` | BN254 G1 addition | 128 bytes | 64 bytes |
| `0x07` | BN254 G1 scalar multiplication | 96 bytes | 64 bytes |
| `0x08` | BN254 pairing check | `192 * k` bytes | 32 bytes |

### Encoding

- G1 points use two 32-byte big-endian field elements `(x, y)`
- G2 points use four 32-byte big-endian field elements `(x_imag, x_real, y_imag, y_real)`
- Scalars use one 32-byte big-endian integer
- The point at infinity remains encoded as zero bytes

This matches the current EIP-196 and EIP-197-compatible interface exposed by TRON.

### Execution Model

When the TVM resolves addresses `0x06`, `0x07`, or `0x08`, it checks:

1. `VMConfig.allowRustZkPrecompiles()`
2. `NativeZkBridge.isRustAvailable()`

If both are true, execution is routed to the Rust-backed precompile implementation. Otherwise, the current Java BN128 implementation is used.

### Native Bridge

`NativeZkBridge` provides:

- `rustBn254Add(byte[] input)`
- `rustBn254ScalarMul(byte[] input)`
- `rustBn254Pairing(byte[] input)`
- `warmup()`
- `isRustAvailable()`

At node startup, enabling `allowRustZkPrecompiles` triggers native warmup so the first live transaction does not absorb JNI initialization latency.

### Error Handling

- Invalid input returns an empty byte array for add and mul
- Invalid pairing input returns `false`
- Native loading failures do not crash the node; they disable the Rust path and fall back to Java
- Rust panics are caught before they cross the JNI boundary

### Energy Costs

The proposal keeps the current TRON energy schedule:

| Operation | Energy |
|-----------|--------|
| ecAdd | 150 |
| ecMul | 6,000 |
| ecPairing | `80,000 * k + 100,000` |

Maintaining the current schedule avoids introducing a pricing change at the same time as the implementation change.

## Rationale

### Why JNI?

The pairing win only matters if the call remains in-process. A sidecar or RPC design would add avoidable serialization and round-trip overhead to each precompile invocation. JNI keeps the TVM call path short and lets the node preserve the performance benefit of native pairing.

### Why Rust and arkworks-rs?

`arkworks-rs` is a production-grade cryptography library already used across the ZK ecosystem. It provides correct BN254 arithmetic, subgroup-aware point handling, and a clean path for future precompiles such as BLS12-381 or Poseidon.

### Why a Feature Flag?

This is an implementation swap inside a consensus-sensitive component. The flag enables:

- staged rollout on private or validator-operated nodes
- instant rollback to the Java path
- A/B benchmarking on the same client implementation

### Why Keep the Existing Java Path?

The Java implementation is still valuable as the default and fallback behavior. If the native library is missing or misconfigured, the node should keep running.

## Backwards Compatibility

This proposal is backward compatible at the smart-contract interface level:

- same precompile addresses
- same input and output encoding
- same observable failure mode
- feature flag defaults to off

Existing contracts that call `0x06`, `0x07`, or `0x08` do not need to change.

## Test Cases

Implementation work validated the following cases:

- Rust unit tests for add, mul, pairing, encoding round-trips, modulus reduction, associativity, bilinearity, and invalid inputs: `26 passed`
- Routing tests confirming the Rust path only activates when both the feature flag and native availability are true
- Energy schedule tests confirming Rust precompile wrappers match the existing Java schedule
- Private-node A/B benchmark showing Java pairing timeout and Rust pairing success
- Groth16 verification using a real `circom` / `snarkjs` proof:
  - valid proof for `y = x * x` with `x = 3, y = 9` -> `true`
  - same proof with invalid public input `10` -> `false`

## Implementation

Running code for this proposal:

- `java-tron` PR: https://github.com/anishnarang9/java-tron/pull/1
- companion project branch: https://github.com/anishnarang9/pennblockchain26/tree/anishnarang9/tron-zk-precompile

The implementation includes:

- Rust BN254 JNI library
- feature-flagged `java-tron` routing
- private-node benchmark harness
- Groth16 verifier contract and proof-generation scripts

## Copyright

Copyright and related rights waived via [CC0](LICENSE.md).
