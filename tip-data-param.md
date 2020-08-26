---
tip: <to be assigned>
title: Accept data parameter in smart contract API
author: kevholder<kevholderx@gmail.com>
discussions-to: https://github.com/tronprotocol/tips/issues/182
status: Draft
type: Standards Track
category: Interface
created: 2020-08-26
---

## Simple Summary

This tip introduces a `data` parameter to the TriggerSmartContract and TriggerConstantSmartContract APIs which represents an ABI encoded function call.

## Abstract

The TriggerSmartContract and TriggerConstantSmartContract APIs accept unencoded parameters (`function_selector`, `parameter`) which are then ABI encoded server-side to generate a `data` value. This tip allows clients to directly pass this `data` value.

## Motivation

It is generally straightforward to port tools and libraries written for EVM-like blockchains to Tron. However, because Tron currently lacks a smart contract API that accepts ABI encoded function calls, working around this problem can require large architectural changes (e.g. this is the case during port efforts of [TheGraph](https://github.com/graphprotocol/graph-node/)).

## Specification

The `data` parameter should be an ABI encoded function call. It should be used as an alternative to the `function_selector` and `parameter` parameters.

## Rationale

To preserve backwards compatibility, an optional `data` parameter was added to the existing `TriggerSmartContract` and `TriggerConstantSmartContract` APIs.

## Implementation

[https://github.com/tronprotocol/java-tron/pull/3369](https://github.com/tronprotocol/java-tron/pull/3369)
