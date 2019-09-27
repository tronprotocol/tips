```
tip: 43
title: TRC-43: Precompiled contract function for signature parallel verification
author: Sh11thead<ksl2945@gmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/43
category: TRC
status: accept
created: 2019-07-10
```
## Simple Summary
A new type of precompiled contract function for signature parallel verification
## Abstract
Add a new type of build-in precompiled contract function for multisign validating instead of the compiled bytecode do the same task.


## Motivation
Since the multi-signature is widely used in Tron, there needs a way for low energy cost and less CPU time multisign validating, the precompiled contract for multi-signature could be a well satisfying solution.

## Specification

Adds a new precompiled contract function, which need 3 arguments input: 
- uint256[] addresses
- uint256[] hashes
- uint256[] signatures

output the result of signature validating would be a bytes32, for example `10100000000000000000000000000000` representing the first signatue and third signatue is correct

for safety concern, the number of signatures is limited to 16


## Energy cost
energy charge for the execution cost 1500 per signature