```
tip: 12
title: TRC-12 Tron event subscribes model
author: jiangyy<jiangyangyang@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/12
status: Final
type: Standards Track
category: TRC
created: 2018-12-20
```

## Simple Summary
This doc describes event subscribe model of Tron.

## Abstract
The following describes a model which is used to subscribe to block chain events, transaction events, contract logs and contract events from Tron FullNode. Developers can set up filters to subscribe to specific events. Plug-ins can be developed to export these events for further development.

## Motivation
This will allow dapps developers or exchange to subscribe any event triggered on Tron. 

## Specification

### Events to subscribe

- **transactionTrigger**, triggered after the transaction is processed
- **blockTrigger**, triggered after a block is inserted into block chain
- **contractLogTrigger**, triggered after smart contract is executed
- **contractEventTrigger**,  triggered after smart contract is executed

### Filter

- **fromBlock**: the beginning of the queried range, it could be set to "", "earliest", "latest" or specified block number, the default value is "latest". "earliest" is the oldest block number from the beginning of the subscription. "latest" is the latest block number when the filter is set.
- **toBlock**: end of the range, it could be set to "", "latest" or specified block number, the default value is "latest".
- **contractAddress**: restricts matches to events created by specific contracts.
- **contractTopics**: The Topic list restricts matches to particular event topics. Each event has a list of topics. Topics match a prefix of that list. An empty element slice matches any.

**Notice**: No support the historical data query.

### Smart Contract log
**contractLogTrigger** is used to represent the object of smart contract log, which has following parameters:

- **transactionId**, transaction id.
- **contractAddress**, contract address.
- **callerAddress**, contract caller address.
- **blockNumber**, the block number of transaction.
- **blockTimestamp**, the packing time of a transaction in block.
- **contractTopics**, list of topics that Log can output in Solidity language.
- **data**, data filed that Log can output in Solidity language.

### Smart Contract event
**contracteventTrigger** is used to represent the object of smart contract log, which has following parameters:

- **transactionId**, transaction id.
- **contractAddress**, contract address.
- **callerAddress**, contract caller address.
- **blockNumber**, the block number of transaction.
- **blockTimestamp**, the packing time of a transaction in block.
- **eventSignature**, signature string of event.
- **contractTopicMap**, It is a map from a topic name to topic value that event can output in Solidity language.
- **data**, data filed that log can output in Solidity language.

 
### Trigger event

- Triggering block event, create a blockTrigger when the block is inserted.
- Triggering transaction event, create a txsTrigger before the transaction is executed.
- Triggeingr smart contract log, create a contractLogTrigger after the contract is executed.
- Triggering smart contract event, create a contractEventTrigger after the contract is executed.

### Send trigger
java-tron sends the trigger to the plugin asynchronously, and the trigger must satisfy the filter condition. The following is a filter example, the block number of the trigger must be between fromBlock and toBlock, the contractAddress must be "AddressA", the topics must include "TopicA", and only the Trigger that satisfies the condition will be sent.

- **fromBlock**: 0x1000000 
- **toBlock**: 0x1200000 
- **contractAddress**: "AddressA" 
- **topics**: ["TopicA"]

## Implementation
The function of the plugin is to implement event dump. Developers can customize it according to their needs, such as Message queue, Kafka, MongoDB or writing to local files.

The plugin is independent of java-tron and is not loaded by default.  It can be enabled by configuring command line parameters. By default, only subscriptions to smart contract event are supported. Developers could subscribe to other triggers by modifying configuration files.

Developers are flexible in defining plug-in configuration files, including message queue server addresses, defined Trigger types, and so on.

Take Kafka plug-in as an example, define the Kafka server address in the configuration file, Kafka topics (corresponding to the Trigger category). After receiving the Trigger sent by java-tron, the plug-in sends the Trigger to the corresponding Kafka topic according to the Trigger category.

The plug-in implements the ILogsFilterPlugin interface, including the initialization and start-up of the plug-in, receiving Trigger, and loading the plug-in according to the configuration file.
