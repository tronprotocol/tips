## Abstract

This document explains a TCP Handshake process that is done by exchanging a pair of `Hello` messages which carry blockchain information. Only when two nodes’ information are compatible can make a successful Handshake.

## Definitions

### Genesis Block
A blockchain is made up by a chain of blocks, each labeled with a unique ID. The very first block generated is called a Genesis Block at the block height of 0.

### Solid Block
Solid Blocks are blocks that are irretrievable. A block cannot be erased from the blockchain once it is solidified. A Solid Block can be calculated using the formula below.

### Head Block
The latest block on the blockchain, representing the max block height.

## Protocol

Handshake occurs immediately after a TCP connection is created. The node initiating the TCP connection request will send a Hello message to its neighbours; neighbours who receive and accept the message will return a Hello message to the sender. Upon completing a Handshake, nodes can have further communication under standard TRON Protocol. Here is the definition of a `Hello` message.
```typescript
message HelloMessage {  
  message BlockId {  
    bytes hash = 1;  
    int64 number = 2;  
  }  
  Endpoint from = 1;  
  int32 version = 2;  
  int64 timestamp = 3;  
  BlockId genesisBlockId = 4;  
  BlockId solidBlockId = 5;  
  BlockId headBlockId = 6;  
  bytes address = 7;  
  bytes signature = 8;  
}
```
`BlockId.hash` consists of the hash value and block height of a specific block; each block has its unique BlockId.

`BlockId.number` indicates the block height.

`from` represents a node identifier and consists of node ip, port and node ID.

`version` represents a p2p version; connections can only be established between nodes with same versions.

`timestamp` indicates the time the connection request is made.

`genesisBlockId` represents the ID of the Genesis Block; connections can only be established between nodes having identical Genesis Blocks.

`solidBlockId` represents the ID of the Solid Block; connections can only be established when the blockchain of one node comprises the Solid Block of the other.

`headBlockId` represents the ID of the Head Block.

## Implements

###  Calculation of Solid Blocks

A block is identified as Solid Block if it has been verified by two thirds of all SRs. The implementation code is demonstrated below.
```typescript
SOLIDIFIED_THRESHOLD = 70;
 
private void updateSolidBlock() {
  List<Long> numbers = consensusDelegate.getActiveWitnesses().stream()
      .map(address -> consensusDelegate.getWitness(address.toByteArray()).getLatestBlockNum())
      .sorted()
      .collect(Collectors.toList());
  long size = consensusDelegate.getActiveWitnesses().size();
  int position = (int) (size * (1 - SOLIDIFIED_THRESHOLD * 1.0 / 100));
  long newSolidNum = numbers.get(position);
  long oldSolidNum = consensusDelegate.getLatestSolidifiedBlockNum();
  if (newSolidNum < oldSolidNum) {
    return;
  }
  consensusDelegate.saveLatestSolidifiedBlockNum(newSolidNum);
}
```

### Hello Message Verification
The Hello message received by the node will be examined in the following steps.
1.  Verify the P2P version. Nodes with different version numbers will be disconnected.
2.  Verify the Genesis Block. Nodes with different Genesis Blocks will be disconnected.
3.  Verify the Solid Blocks. Nodes will be disconnected if the max block height of the Solid Blocks on local blockchain exceeds that of the neighbouring node and the Solid Blocks of the neighbour are not on the chain.
```typescript
if (msg.getVersion() != Args.getInstance().getNodeP2pVersion()) {
  channel.disconnect(ReasonCode.INCOMPATIBLE_VERSION);
  return;
}

if (!Arrays
    .equals(manager.getGenesisBlockId().getBytes(), msg.getGenesisBlockId().getBytes())) {
  channel.disconnect(ReasonCode.INCOMPATIBLE_CHAIN);
  return;
}

if (manager.getSolidBlockId().getNum() >= msg.getSolidBlockId().getNum() && !manager
    .containBlockInMainChain(msg.getSolidBlockId())) {
  channel.disconnect(ReasonCode.FORKED);
  return;
}
```
## Change Log
