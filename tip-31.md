```
tip: 31
title: TRC-31 Trigger constant contract
author: llwslc<llwslc@gmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/31
category: TRC
status: Final
created: 2019-4-3
```
## Abstract

This TIP specifies a new api, which triggers the constant contract without ABI.

## Motivation

Some of contracts are uploaded without the ABI. It is hard to judge whether the function is a constant function or not. So, we must provide an interface for calling the constant function explicitly.  

## Specification

A new api,` triggerConstantContract`, is introduced. 
```
// api.proto
rpc TriggerConstantContract (TriggerSmartContract) returns (TransactionExtention) {}
```

The `triggerConstantContract` parameters are the same as the `triggerContract`.

`triggerConstantContract contract_address method args isHex`

Http interface example:

`curl -X POST  http://127.0.0.1:8090/wallet/triggerconstantcontract -d {"contract_address":"4189139CB1387AF85E3D24E212A008AC974967E561","function_selector":"foo(uint256,uint256)","parameter":"00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000002","owner_address":"41D1E7A6BC354106CB410E65FF8B181C600FF14292"}'`

In case the type of method is not constant will gets error.

## Backwards Compatibility

There are no backwards compatibility concerns.

## Test Cases

1. Trigger the constant method by` triggerConstantContract`.
2. Trigger the non-constant method by `triggerConstantContract`.
