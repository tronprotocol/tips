```
tip: 41
title: Optimize transactionHistoryStore occupancy space#40
author: wubin1<wubin1@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/40
category: TRC
status: Final
created: 2019-5-20
```

## Simple Summary

This doc describes the solution of optimizing transactionHistoryStore occupancy space.

## Abstract

In current storage model, transaction result saves in transaction history store and it occupies the most space.
The optimization merges all transactions in a common block and compression the transaction history space.

## Motivation

TRON database already occupied 163GB and it increases 20G each month. So how to optimize space is very import.

## Specification

TransactionHistory doesn't directly save in transactionHistoryStore after the execution of transactions.
**_transactionHistoryStore.put(trxCap.getTransactionId().getBytes(), transactionInfo);_**

Add transaction history in memory and save in disk after executing one whole block.
 
` transationHistoryCapsule.addTransactionResult(result); 
      if (block.getTransactions().size() != 0) {
       this.transactionHistoryStore.put(ByteArray.fromLong(block.getNum()), block.getResult());
     } `

## Rationale
Saving transaction history for a whole block could reduce duplicate data and protocol buffer compression is more effective for large data.

## Backwards Compatibility

There are no backwards compatibility concerns.

## Test Cases

1. Compare storage size from optimization version and not optimization version.
2. Query function for transaction history

