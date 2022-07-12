```
tip: 54
title: TRC-54: Automatically active non-existent account when transferring TRX/TRC10 asset in a smart contract
author: Jeancky <jiangxinjian@tron.network>
discussions to: https://github.com/tronprotocol/TIPs/issues/54
category: TRC
status: Final
created: 2019-08-09
```
## Abstract

Currently in TRON's smart contract, when transferring to a non-existent address, the transaction will be failed. This may cause inconvenience to some DApp developers. Let's discuss whether automatic creation of non-existent address should be allowed during contract transfer. Of course, contract caller need to pay the corresponding fee.

## Motivation

At TRON, when these system GRpc API transferContract, transferAssetContract are called, an non-existent address is automatically activated. However, when transferring with transfer and transferToken in a smart contract, the non-existing address is not automatically activated. This can make the user experience inconsistent, and it can also cause problems for developers.

## Specification

Before implementing this function, we need to consider that when the address is activated, the instruction will charge an additional 0.1 TRX fee.

There are many ways to do this, here are two possible ways:

1. Directly modify the semantics of transfer, transferToken, allowing the creation of non-existing addresses. Its drawback is that it may affect contracts that have relied on the "contract will be reverted when transfer to non-existing address" feature. Bringing unknown risks to them.
2. Adding a new auto-activation instruction in the new TRON solidity compiler, and let the compiler to automatically insert this instruction before transfer/transferToken when generating bytecode. This method allows a version to support this behavior. But when compiled with an old compiler, it will never be supported.

## Rationale

In terms of instruction charging, the energy price is an adjustable variable. How to accurately charge 0.1TRX needs to be discussed.

Regardless of the implementation method, we need to consider whether it will have an unknown impact on existing contracts. Also be consistent with the GRPC API.

## Backwards Compatibility

1. In terms of energy consumption, it needs to be consistent with the system GRPC interface.
2. If we want to do that, we need to review the impact of each implementation on existing contracts.
3. One of these implementations relies on TRON's Solidity compiler update, which is not compatible with historical compiler versions.
