---
tip: <to be assigned>
title: Native BN254 Precompiles via Rust FFI
author: Anish Narang (@anishnarang9), Blockchain@Maryland
discussions-to: https://github.com/tronprotocol/tips/issues/846
status: Draft
type: Standards Track
category: VM
created: 2026-03-24
---

## Simple Summary

Replace TRON's current Java BN254 precompile path for `0x06`, `0x07`, and `0x08` with a native Rust-backed implementation while preserving the same addresses, adopting exact EIP-196/EIP-197 edge-case semantics, and activating the new path through deterministic committee governance.

## Abstract

This TIP proposes a native implementation of the BN254 elliptic curve precompiles at addresses `0x06`, `0x07`, and `0x08`. The proposal preserves the existing TRON contract interface, adopts exact EIP-196/EIP-197 calldata handling semantics, and keeps conservative precompile pricing. Activation is controlled by the `allowRustZkPrecompiles` committee parameter and takes effect at a governance boundary rather than through per-call local switching.

On the fresh private-node workload captured in the companion repository's tracked evidence, the native path completed a real Merkle-membership Groth16 verification transaction in `1020.37 ms` with `502,878` total energy, while the current generic Java path hit `OUT_OF_TIME` after `123.3 ms` of execution and never completed the transaction.

## Motivation

TRON already has specialized shielded-transaction zk support through TRONZ / TIP-137. This TIP is not about replacing that system. It is about the generic BN254 precompile path exposed through `0x06`, `0x07`, and `0x08`.

For that generic path, the current Java implementation is too slow for practical Groth16 verification on a real Merkle-membership workload. On the fresh 2026-03-27 verifier-run capture in the companion repository:

| Operation | Java (current generic path) | Rust (proposed path) | Speedup |
|-----------|-----------------------------|----------------------|---------|
| ecAdd (`0x06`) | `93 us` | `5 us` | **18.6x** |
| ecMul (`0x07`) | `4,606.5 us` | `63.8 us` | **72.2x** |
| ecPairing (`0x08`) | `98,203 us` | `1,406.8 us` | **69.8x** |

In the tracked benchmark summaries at [groth16-e2e-rust.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-rust.json) and [groth16-e2e-java.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-java.json), the Rust path completed a real-transaction Groth16 verification with:

- txid `8c35e621bd803c06f00443c741d4045c635886bb22de74b4327e6265687e18b4`
- `502,878` total energy
- `1020.37 ms` wall time

The Java path hit `OUT_OF_TIME` instead:

- `123.3 ms` until failure
- `class org.tron.core.vm.program.Program$OutOfTimeException : CPU timeout for 'SWAP1' operation executing`

The same companion repository also tracks valid and invalid Merkle-membership proof outcomes in [groth16-valid-invalid-tx.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-valid-invalid-tx.json). That workload is a depth-20 Poseidon Merkle-membership circuit with `11,332` constraints and two public inputs (`root`, `nullifierHash`). The point of the TIP is narrow and concrete:

- the current generic BN254 path is not practical for this workload
- the proposed native path is

Fresh proof-verification captures from the same run:

- valid proof txid `48910ab671599bbc7a166d235a828cc3d2440267a6287448e895d8c78280699e` -> `true`
- invalid-root txid `eaa2bee3c225885f8688159de102502338cd4fc5d98e99ba8178d804a3b51ef4` -> `false`
- both proof-verification transactions used `502,878` total energy

## Specification

### Precompile Addresses

| Address | Operation | Input | Output |
|---------|-----------|-------|--------|
| `0x06` | BN254 G1 Addition | two G1 points | one G1 point |
| `0x07` | BN254 G1 Scalar Multiplication | one G1 point and one scalar | one G1 point |
| `0x08` | BN254 Pairing Check | `k` G1/G2 pairs | 32-byte boolean |

### Point Encoding

**G1 points** use 64 bytes: two 32-byte big-endian unsigned integers `(x, y)` in `Fq`. The point at infinity is encoded as 64 zero bytes.

**G2 points** use 128 bytes: four 32-byte big-endian unsigned integers `(x_imag, x_real, y_imag, y_real)` in `Fq2`. This follows the EIP-197 ordering.

**Scalars** use one 32-byte big-endian unsigned integer.

### Calldata Semantics

#### ecAdd (`0x06`)

- The operation consumes the first 128 bytes of calldata.
- If calldata is shorter than 128 bytes, it is virtually zero-padded.
- If calldata is longer than 128 bytes, surplus bytes are ignored.
- The return value is a 64-byte G1 point.

#### ecMul (`0x07`)

- The operation consumes the first 96 bytes of calldata.
- If calldata is shorter than 96 bytes, it is virtually zero-padded.
- If calldata is longer than 96 bytes, surplus bytes are ignored.
- The return value is a 64-byte G1 point.

#### ecPairing (`0x08`)

- Calldata length must be a multiple of 192 bytes.
- Empty calldata is valid and returns 32 bytes with the final byte set to `1`.
- A successful call returns 32 bytes:
  `0x...01` if the product of pairings equals the identity
  `0x...00` otherwise
- Malformed pairing calldata causes the call to fail rather than returning a logical `false` word.

These calldata rules are intended to match EIP-196 and EIP-197 exactly.

### Error Handling

- For `ecAdd` and `ecMul`, invalid points or deserialization failures cause call failure and consume the supplied energy.
- For `ecPairing`, malformed input length, invalid points, subgroup failures, and deserialization failures cause call failure and consume the supplied energy.
- A structurally valid Groth16 proof with the wrong public inputs must still return a logical `false` result at the verifier layer; that is not treated as malformed precompile input.

### Energy Costs

| Operation | Energy Cost | Ethereum Gas (EIP-1108) |
|-----------|-------------|--------------------------|
| ecAdd | `150` | `150` |
| ecMul | `6,000` | `6,000` |
| ecPairing | `80,000 * k + 100,000` | `34,000 * k + 45,000` |

The pairing price remains conservative in this TIP. This proposal is about making the generic BN254 path executable and performant enough to support real Groth16 workloads. It is not a pairing-price-reduction proposal.

### Activation And Governance

Activation is controlled by the `allowRustZkPrecompiles` committee parameter:

- `0` (default): use the current Java path
- `1`: use the native BN254 path

Normative activation rules:

- Governance activation takes effect at the next applicable maintenance period boundary.
- Once the parameter is active, validating nodes must run a compatible binary with the native implementation available.
- Activated validator deployments must not silently fall back to the Java path.
- If the parameter is active and the native implementation is unavailable, the node must fail fast / refuse to operate in the activated mode rather than silently producing divergent behavior.
- Rolling back from `1` to `0` requires another governance action and follows the same maintenance-period timing.

Non-normative note:

Private-node and pre-activation benchmark environments may still use local toggles to compare the Java and native paths. That benchmark setup is not itself part of the consensus specification.

## Rationale

### Why keep the existing addresses?

The proposal targets the generic BN254 interface already exposed through `0x06`, `0x07`, and `0x08`. Reusing those addresses keeps contract integrations straightforward and avoids fragmenting the VM surface area.

### Why insist on exact EIP calldata semantics?

The main value of matching Ethereum here is not branding. It is predictability. Exact calldata semantics make malformed-input behavior boring, testable, and portable across tooling and verifier generators that already target the EIP-196/EIP-197 model.

### Why keep conservative pricing?

The benchmark evidence in the companion repository proves a large performance improvement and shows that a real Merkle-membership Groth16 workload becomes executable on the native path. That is a strong claim already. It does not by itself prove that pairing should immediately be repriced to Ethereum's post-EIP-1108 levels on TRON mainnet.

### Why focus on verifier-run timings instead of only direct precompile microbenchmarks?

The companion repository tracks both:

- direct precompile benchmark captures in [precompile-benchmark-rust.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/precompile-benchmark-rust.json) and [precompile-benchmark-java.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/precompile-benchmark-java.json)
- in-verifier timings inside the real Groth16 benchmark in [groth16-e2e-rust.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-rust.json) and [groth16-e2e-java.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-java.json)

The verifier-run timings are the stronger evidence for this TIP because they measure the exact workload the proposal is trying to unblock. The direct precompile microbenchmarks remain useful as supporting evidence, but they use a different benchmark contract and should not be treated as the same measurement context.

### Current-Verifier Example

The current verifier example in [Groth16Verifier.sol](https://github.com/anishnarang9/pennblockchain26/blob/main/contracts/Groth16Verifier.sol) performs:

- `2` scalar multiplications
- `2` additions
- `1` pairing check over `4` pairs

Under this TIP's current pricing that is:

- `2 * 6,000 = 12,000`
- `2 * 150 = 300`
- `80,000 * 4 + 100,000 = 420,000`

Total: **`432,300` energy** for the current verifier's precompile calls.

This is a verifier-specific example, not a generic formula for every Groth16 verifier.

## What This Unlocks

This TIP lays the foundation for application classes that depend on practical generic BN254 verification on TRON:

| Application Class | Why This Matters |
|-------------------|------------------|
| ZK rollups | Batch-validity verification depends on practical pairing performance |
| Shielded transfer systems | Merkle-membership and nullifier-style Groth16 verification becomes viable on the generic path |
| Cross-chain zk verification | On-chain proof verification becomes feasible without the current generic-path timeout profile |
| Identity / credential proofs | Generic BN254 verifiers become realistic building blocks instead of benchmark-only experiments |
| Verifiable computation | Generic Groth16 proof verification becomes part of the usable VM surface |

This section is intentionally foundation-oriented. The benchmark evidence in the companion repository shows a major technical improvement. It does not claim optimal economics for every one of these use cases today.

## Backwards Compatibility

This TIP is backward compatible at the contract interface level:

- same precompile addresses
- same BN254 point/scalar encoding
- exact EIP-196/EIP-197 calldata semantics
- default governance state remains off

Existing contracts that already target these addresses do not need to change their call sites.

## Security Considerations

1. **Deterministic activation**: consensus-visible execution must not depend on local library availability after governance activation.
2. **Malformed input handling**: pairing malformed-input cases must fail the call rather than collapsing into a logical `false` result.
3. **Point validation**: both G1 and G2 points require curve and subgroup checks.
4. **JNI boundary safety**: the native bridge must contain panics and surface failure cleanly.
5. **Conservative pricing**: the TIP intentionally keeps a conservative pairing cost until separate pricing evidence is available.

## Test Cases

### Calldata Handling

#### ecAdd (`0x06`)

1. Empty / short input is zero-padded.
2. Surplus bytes are ignored.
3. Identity plus identity returns identity.
4. Generator plus identity returns generator.
5. Invalid points fail the call.

#### ecMul (`0x07`)

1. Empty / short input is zero-padded.
2. Surplus bytes are ignored.
3. Generator times zero returns identity.
4. Generator times one returns generator.
5. Invalid points fail the call.

#### ecPairing (`0x08`)

1. Empty input returns true.
2. Valid negation check returns true.
3. Malformed length fails the call.
4. Invalid G1/G2 points fail the call.
5. Structurally valid but incorrect verifier inputs return logical false at the verifier layer.

### Empirical Validation

The tracked evidence pack for this draft lives in the companion repository:

- [precompile-benchmark-rust.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/precompile-benchmark-rust.json)
- [precompile-benchmark-java.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/precompile-benchmark-java.json)
- [groth16-e2e-rust.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-rust.json)
- [groth16-e2e-java.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-e2e-java.json)
- [groth16-valid-invalid-tx.json](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/groth16-valid-invalid-tx.json)
- [benchmark-methodology.md](https://github.com/anishnarang9/pennblockchain26/blob/main/tip/evidence/benchmark-methodology.md)

Key fresh values from that evidence pack:

- Rust verifier run: `SUCCESS`, `502,878` energy, `1020.37 ms`
- Java verifier run: `OUT_OF_TIME`, `123.3 ms`
- Rust verifier-path pairing average: `1,406.8 us`
- Java verifier-path pairing average: `98,203 us`
- Valid proof result: `true`
- Invalid-root result: `false`

## Implementation

This section is non-normative.

Companion implementation and evidence repository:

- [anishnarang9/pennblockchain26](https://github.com/anishnarang9/pennblockchain26)
- [zk_precompile/](https://github.com/anishnarang9/pennblockchain26/tree/main/zk_precompile) — native BN254 implementation
- [java/](https://github.com/anishnarang9/pennblockchain26/tree/main/java) — reference JNI bridge and wrapper classes
- [contracts/Groth16Verifier.sol](https://github.com/anishnarang9/pennblockchain26/blob/main/contracts/Groth16Verifier.sol) — current verifier used for the Groth16 example
- [scripts/](https://github.com/anishnarang9/pennblockchain26/tree/main/scripts) — benchmark and demo tooling
- [tip/evidence/](https://github.com/anishnarang9/pennblockchain26/tree/main/tip/evidence) — tracked benchmark and demo evidence cited by this TIP

## Copyright

Copyright and related rights waived via [CC0](LICENSE.md).
