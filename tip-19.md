```
tip: 19
title: TRC-19 Deferred transaction
author: jiangyy jiangyangyang@tron.network
discussions to: https://github.com/tronprotocol/tips/issues/19
status: Deferred
type: Standards Track
category: TRC
created: 2019-01-30
``` 

## Simple Summary

Deferred transaction will be supported in Tron. Transaction can be delayed and revoked before it expires. This would provide developers with more flexible and efficient experience.


## Abstract

Currently, the transaction in Tron will be executed immediately. In certain scenarios, developers need to trigger transactions at a specified time and be able to cancel the transaction before it expires. It is necessary to take into account the potential security issue caused by deferred transactions, such as transaction congestion attack. Fee for deferred transactions should also be modified.

## Motivation

This will allow developers to execute deferred transactions in Tron. More business scenarios can be satisfied.

## Specification

**Transaction Structure**

Add "delaySeconds" in the transaction structure which is defined in Tron.proto.

MessageTransaction{
Message raw{

Bytes ref_block_bytes = 1;
Int64 ref_block_num = 3;
Bytes ref_block_hash = 4;
Int64 expiration = 8;
Repeated authority auths = 9;
// data not used
Bytes data = 10;
// Only support size = 1, repeated list here for extension
Repeated Contract contract = 11;
// scripts not used

Bytes scripts = 12;
Int64 timestamp = 14;
Int64 fee_limit = 18;
Int64 delaySeconds = 19; // seconds of delay
}
}

"delaySeconds" is placed in the raw field, so that it could be protected using permissions.

Message DeferredTransaction{
Bytes transactionId = 1;
Int64 publishTime = 2;
Int64 delayUntil = 3;
Int64 expiration = 4;
Bytes senderAddress = 5;
Bytes receiverAddress = 6;
Transaction transaction = 7;
}

Deferred Transaction Stored in Chain.

**DeferredTransactionStore**

For storing delayed transactions waiting to be executed, including the following fields:

Transactionid
Delay_until// The time at which the transaction is expected to execute
Publish // Publish Time
Expiration // delayed transaction expiration time
Sender // sender address
Payer // receiver address

**DeferredTransactionIdIndexStore**

An index database of delayed transactions with transaction ID as key is used to quickly retrieve delayed transactions.

**Settings/Cancels/Trigger**

Wallet and java-tron need to be modified for transaction types that support delayed transactions

1. AccountUpdateContract
2. TransferContract
3. TransferAssetContract
4. AccountCreateContract
5. UnfreezeAssetContract
6. FreezeBalanceContract
7. UnfreezeBalanceContract
8. WithdrawBalanceContract
9. UpdateAssetContract
10. SetAccountIdContract
11. UpdateSettingContract
12. UpdateEnergyLimitContract
13. AccountPermissionUpdateContrac

**Cancellation of deferred transactions**

CancelDeferred Transaction, entered as transactionid, is deleted from the database if the transaction has not expired when fullnode is executed. Cancellation of transactions is linked.

Cancellation of delayed transactions requires authorization, and only an account created for delayed transactions can be authorized to cancel.

**Delayed Transaction Trigger**

The execution of a delayed transaction includes two stages: submitting the delayed transaction and executing the delayed transaction.

Users need to login account on Wallet-cli , then transaction would include the account address.

**Delayed transaction submitted**

When the fullnode node receives the delayed transaction, the transaction data is inserted into the Deferred Transaction Store, indexed and inserted into the Deferred Transaction IdIndexStore.

**Delayed transaction execution**

When a transaction expires, the transaction data is read from the Deferred Transaction Store, the transaction is executed, and the records in the Deferred Transaction Store are deleted.

Note: The transaction ID and transaction receipt of the two transaction records are different. For example, the Wallet-cli side executes sendcoin and generates a transaction ID of TransactionA.

When a delayed transaction is executed for the first time, the corresponding transaction ID is TransactionA, and a new transaction ID is generated for the second execution to identify the transaction that is actually executed.

**Default Parameter & Configuration**

DEFERED_TRANSACTION_FEE//Cost of creating delayed transactions, default 0.1 TRX
CANCEL_DEFERED_TRANSACTION_FEE//Cost of cancelling delayed transactions, default 0.05 TRX
MAX_DEFERED_TRANSACTION_PROCESS_TIME // Maximum processing time for delayed transactions per block, default to 100 ms
All three parameters can be modified by proposals.

Delayed transactions are charged according to the number of days, and the cost per day is 0.1 trx. Assuming a delay of 10 days, the total charge is 10 * 0.1 TRX = 1 trx.

**Generate block logic**

The priority of deferred transaction is higher than that of ordinary transaction. First, the deferred transaction due is executed, and then the ordinary transaction is executed.

The total execution time limit of delay transaction is set to 100 ms to prevent congestion attack.

Pressure measurement is used to verify the maximum number of delayed transactions per block, and the setting of timeout parameters can be adjusted.

**Wallet/browser support**
Add RPC / HTTP interface settings and cancel transaction.
Transaction query command, which can display fields related to delayed transactions.

GetTransactionById: Enter the transactionid returned by wallet-cli and return the first record of the delayed transaction.

GetDeferredTransactionById: Enter the transactionid returned for wallet-cli, return the real transaction information, corresponding to the second record of the delayed transaction.

**Proposal support**
In order to dynamic change config, we add three new proposals to support the deferred transaction.
Proposal 24: change the deferred transaction fee.
Proposal 25: change cancel fee of the deferred transaction.
Proposal 26: change max deferred transaction process time in one block.


## Rationale


## Implementation


