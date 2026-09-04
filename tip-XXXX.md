---
tip: <TIP Number (to be assigned)>
title: Add input and output fields to InternalTransactions
author: @roseshahar
discussions-to: https://github.com/tronprotocol/tips/issues/816
status: Draft
type: Standards Track
category: Core
created: 2026-01-16
---

## Simple Summary
Include the `input` (call data) and `output` (return data) fields in TRON's `InternalTransactions` to provide complete execution traces.

## Abstract
This TIP proposes an update to the TRON protocol's internal transaction data structure. By adding `input` and `output` fields to `InternalTransactions`, the network will store the data sent to internal function calls and the resulting return values. This change enables indexers, block explorers, and developers to fully reconstruct the execution flow of complex smart contract interactions, such as factory-based deployments and nested contract calls.

## Motivation
Currently, TRON does not persist the `input` and `output` fields of internal transactions in its database. This creates a significant visibility gap for:
1.  **Contract Factories:** It is difficult to identify and verify contract instances deployed via a factory contract without the deployment `input` data.
2.  **Complex Call Chains:** Developers cannot see the specific arguments passed to or the values returned from internal contract-to-contract calls.
3.  **Indexer Accuracy:** External indexers are forced to re-execute transactions locally to find this data, which is resource-intensive and prone to inconsistencies.

Adding these fields aligns TRON with standard EVM "trace" behaviors, making the ecosystem more transparent and developer-friendly.

## Specification
The `InternalTransaction` structure and the corresponding database storage logic in `java-tron` will be updated to include two new fields:

* **`input`**: A `bytes` field containing the data (parameters) passed during the internal call.
* **`output`**: A `bytes` field containing the return data produced by the internal call.

### Protocol Changes
The internal logic that captures `InternalTransactions` during VM execution will be modified to capture the call data and return data buffers and commit them to the node's database alongside existing fields (like `caller_address`, `transferTo_address`, and `note`).

## Rationale
The design choice to store these fields directly in the database (as opposed to just logging them) is driven by the need for high-performance indexing. While this increases the storage footprint of the node, the benefits to the developer ecosystem and the accuracy of data provided by explorers like TRONSCAN outweigh the storage costs.

## Backwards Compatibility
This is a **non-breaking, additive change**:
* **Consensus:** This change does not affect the consensus layer or the validation of blocks. It is a modification to how historical execution data is recorded.
* **Storage:** Existing `InternalTransactions` in the database will not have these fields. Only new internal transactions generated after the implementation is active will include the `input` and `output` data.

## Implementation
The implementation for this TIP can be found in the following PR:
[https://github.com/tronprotocol/java-tron/pull/6511](https://github.com/tronprotocol/java-tron/pull/6511)

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).