## Simple Summary

A new contract creation function called CREATE2.

## Abstract

A new method of creating a contract is proposed where the resulting address can be determined by parties ahead of time.

## Motivation

Allows interactions to (actually or counterfactually in channels) be made with addresses that do not exist yet on-chain but can be relied on to only possibly eventually contain code that has been created by a particular piece of init code. Important for state-channel use cases that involve counterfactual interactions with contracts.

## Specification

Adds a new opcode at 0xf5, which takes 4 stack arguments: endowment, memory_start, memory_length, salt. Behaves identically to CREATE, except using `addressPrefix ++ keccak256(address ++ salt ++ keccak256(init_code))[12:]` to create a new contract address. `addressPrefix` is `0x41` forT
The CREATE2 has the same `engery` schema as `CREATE`, but also an extra `hashcost` of `GSHA3WORD * ceil(len(init_code) / 32)`, to account for the hashing that must be performed. The `hashcost` is deducted at the same time as memory-expansion engery and `Creat`e is deducted: before evaluation of the resulting address and the execution of ``.

- address is always 21 bytes,
- salt is always 32 bytes (a stack item).
- `keccak256(init_code)` 32 bytes

The preimage for the final hashing round is thus always exactly 85 bytes long.

## Rationale

**Address formula**
- Because instruction CREATE mainly depends on `trxHash`, the CREATE2 addresses will not collide with CREATE addresses.
    - Deploy contract: `addressPrefix ++ keccak256(trxHash ++ txOwnerAddress)[12:]`
    - in internal transaction: `addressPrefix ++ keccak256(trxHash ++ nonce)[12:]`
- Ensures that the hash preimage has a fixed size,

**Engery cost**
Since address calculation depends on hashing the `init_code`, it would leave clients open to DoS attacks if executions could repeatedly cause hashing of large pieces of `init_code`, since expansion of memory is paid for only once. This TIP uses the same cost-per-word as the `SHA3` opcode.
