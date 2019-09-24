```
tip: 34
title: TRC-34 Event subscribe to support contract without ABI
author: wubin1<wubin1@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/34
category: TRC
status: final (non-Core)
created: 2019-4-19
```
## Simple Summary
This tip is about event subsribe to support contract without abi. It is very convenient for developers who need to upload self ABI.

## Abstract
To support contract without ABI,  contract log parsing is separated from java-tron main program.
Moreover, developers could upload self ABI string to parse contract log and contract event,  which could be more convenient to support some contracts without ABI.

## Motivation

The contract does not need ABI anymore after the introduction of [triggerConstantContract](#31 ) api, so tron-eventquery service could support developers to upload ABI and parse contract log and contract event.

## Specification
In order to support contract without ABI, contract log parsing is separated from java-tron main program and we parse contract log in event plugin.
In addition,  the function of parse contract log is configurable. It's is true by default. 

event.subscribe = {
      contractParse = true,
    ......

If it is false, we only pass  the  raw data to developers who subscribe events.

Moreover, event query service adds three new http api for supporting developers to developers parse contract log and contract event by self upload ABI string.

Developers could subscribe triggers more conveniently.  

## Backwards Compatibility

There are no backwards compatibility concerns.

## Test Cases

1. Emitting events from contract that without ABI.
2. Emitting events from contract that with ABI.
