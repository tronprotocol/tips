```
tip: 44
title: TRC-44 Address.isContract instructions
author: llwslc<llwslc@gmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/44
category: TRC
status: Final
created: 2019-07-10
```
## Simple Summary

To provide a new opcode, which returns the type of the address.

## Abstract

This TIP specifies a new opcode, which determines whether the address type is a contract address.

## Motivation

Some contracts need to limit its callers, such as some functions can only be called by the user, not by the contract.

## Specification

A new opcode, `ISCONTRACT`, is introduced, with number `0xD4`. The `ISCONTRACT` takes one argument from the stack, pushes to the stack the boolean value whether the address type is a contract address.

In case the address does not exist `false` is pushed to the stack.

example:
```
contract Test {
    function checkAddr(address addr) view public returns (bool) {
        return addr.isContract;
    }
}
```
The energy cost of the` ISCONTRACT` is 400.

## Backwards Compatibility

There are no backwards compatibility concerns.

## Test Cases

1. The `ISCONTRACT` of a contract address is `true`.
2. The `ISCONTRACT` of an account address is `false`.
3. The `ISCONTRACT` of a non-existent address is `false`.
4. The `ISCONTRACT` of a precompiled contract is `false`.
5. The `ISCONTRACT` of self address in constructor function is `true`.
6. The `ISCONTRACT` of a selfdestructed contract address is `false`.

