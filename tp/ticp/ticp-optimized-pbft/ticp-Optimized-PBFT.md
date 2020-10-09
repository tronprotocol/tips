```
ticp: 2
title: Optimized PBFT Consensus Algorithm
author: @lvs007
type: Tron Inter-blockchain Communication Protocol
category: TRC
status: Draft
created: 2019-12-12
```

## Summary

In an effort to cut average confirmation time and ensure provable finality for cross-chain services, we plan to introduce into TRON's consensus algorithm an optimized PBFT consensus algorithm.

## Abstract

Practical Byzantine Fault Tolerance is a consensus algorithm used in asynchronous distributed system that keeps the entire distributed system available on the condition of partition failure happening. Total node count (n) and failed node count (f) satisfy the following relation: f <= ⌊(n-1)/3⌋

A standard PBFT algorithm requires 5 types of messages:

- VIEW_CHANGE

- REQUEST

- PRE_PREPARE

- PREPARE

- COMMIT

Based on the current consensus algorithm of TRON, we propose an optimized PBFT algorithm that requires 3 types of messages:

- PRE_PREPARE

- PREPARE

- COMMIT

Meanwhile, based on the CAP theorem for distributed systems, TRON plans to moderately improve Consistency of the system while ensuring Availability by assigning 3 roles to all nodes in the PBFT consensus algorithm:

- Super representative: nodes that produce blocks

- Verifier: nodes that trigger the PBFT consensus procedure for blocks produced by SRs

- Full node: normal nodes that supervise the consensus behavior above

## Motivation

In the current DPoS consensus mechanism of TRON Protocol, the average confirmation time for one block is equal to (2/3 * Number of SRs) slots. With the adoption of PBFT consensus algorithm, however, the confirmation time will shrink significantly to only 1 or 2 slots if the network environment is good enough.

To achieve cross-chain decentralization, blockchains must be mutually verifiable and therefore able to verify cross-chain transactions. To this end, SPV is undoubtedly the most succinct approach as lightweight clients require only block header information to complete verification.

To execute minimum transactions and thus achieve provable finality of a block header, PBFT consensus algorithm featuring strong consistency is a good fit as provable finality can be attained with as few data as possible.

## Rationale

After the block produced and broadcast by the SR reaches Verifiers and gets validated, Verifiers will broadcast a prepare message with their signatures to trigger the PBFT consensus procedure. At this point, other nodes in the network can verify the finality of the current block through the consensus algorithm.

Such round of PBFT consensus procedure will be conducted every time a block is processed. For blocks reaching a consensus, their PBFT information will be saved to local database through putBlockSignData function and ready for verification in the lightweight clients.

Threshold signature scheme can help handle multisignature schemes related to the PBFT consensus algorithm. Using threshold signature schemes in the signature module and the verification module will make the entire system simpler and more efficient. Therefore, we plan to utilize this technology in the upcoming versions.

## Specification

### Comparison with traditional PBFT:

As illustrated in the two figures below, the first phase is block broadcasting, which is equivalent to the pre_prepare phase of traditional PBFT; the second is the vote stage where blocks are verified, equivalent to the prepare phase of traditional PBFT; the third phase is verifying vote results, equivalent to the commit phase of
traditional PBFT. Below are the details:

1. SRs will broadcast the message after producing a block

2. Upon receiving the broadcast block, Verifiers will validate it, then sign and broadcast the result

3. Upon receiving signed prepare messages from more than 2/3+1 Verifiers, a commit message will be generated, which will then be signed and broadcasted by Verifiers

4. If nodes receive signed commit messages from more than 2/3+1 Verifiers, it is deemed that the current block can never be reverted

Each node only votes once on blocks of the same height; messages already received will be discarded right away without being processed. Meanwhile, if the node fails to confirm the prepare messages upon receiving commit messages, the current commit messages need to be cached.

TRON's optimized PBFT consensus algorithm also features a Timeout mechanism. If a round of PBFT algorithm fails to reach finality within a given period of time, all data related to this round will be cleared by all nodes. But one difference from the traditional PBFT is that TRON will not re-initiate this round.

<center>Figure 1</center>

![](https://github.com/tronprotocol/tips/raw/master/tp/ticp/ticp-optimized-pbft/pbft-1.png)

<center>Figure 2</center>

![](https://github.com/tronprotocol/tips/raw/master/tp/ticp/ticp-optimized-pbft/pbft-2.png)

A SR can be acted as Verifiers role, both of those two run on the same server. 

For fullnode,  it only receive pbft message from network and not participate in consensus process. Once fullnode receive 2f+1 commit pbft message, it will confirm blocks. 

### Datatypes

Firstly, we need to define a data structure for PBFT signature which encapsulates SR signature data.

```typescript

public class PbftSignCapsule

```

Each vote is recorded as a message, so we define a message structure,
PbftMessage, to cover all vote messages.

```typescript

public class PbftMessage

```

The main aim of this data structure is to save signed commit messages and collect information on SRs who are signing current data.

```typescript

public class DataSign

```

PbftBaseMessage encapsulates PbftMessage and supports features such as signing validation messages and creating prepare and commit messages.

```typescript

public class PbftBaseMessage

```

PbftMessage: Type indicates the vote message type.

Raw indicates the data that need to be signed, which mainly include: pbftMsgType, blockNum, time, publicKey, data and data_sign.

Sign indicates SR's signature on the entire raw data.

```typescript

message PbftMessage {

enum Type {

VIEW_CHANGE = 0;

REQUEST = 1;

PREPREPARE = 2;

PREPARE = 3;

COMMIT = 4;

}

message Raw {

Type pbftMsgType = 1;

int64 blockNum = 2;

int64 time = 3;

bytes publicKey = 4;

bytes data = 5;

bytes data_sign = 6;

}

Raw raw_data = 1;

bytes sign = 2;

}

```

DataSign is mainly used to store signed messages.

Data indicates the data signed by SRs; sign indicates SR's signature on data. These two concepts correspond to data and data_sign in PbftMessage.

```typescript

message DataSign {

bytes data = 1;

repeated bytes sign = 2;

}

```

### Required functions

Set the signature data of the current epoch SR list. Cycle means being currently in that epoch.

```typescript

public boolean putSrSignData(long cycle, PbftSignCapsule item)

```

Get the signature data of the current epoch SR list

```typescript

PbftSignCapsule getSrSignData(long cycle)

```

Set the signature data of the current block (namely the SR signature list)

```typescript

public void putBlockSignData(long blockNum, PbftSignCapsule item): Set

```

Get the signature data of the current block (namely the SR signature list)

```typescript

public PbftSignCapsule getBlockSignData(long blockNum)

```

Each vote is recorded as a message, so we define a message structure, PbftMessage, to cover all vote messages; please see full details under data structure.

```typescript

public class PbftMessage

```

The main aim of this data structure is to save signed commit messages and collect information on SRs who are signing current data; please see full details under data structure.

```typescript

public class DataSign

```

PbftBaseMessage encapsulates PbftMessage and supports features such as signing validation messages and creating prepare and commit messages

```typescript

public class PbftBaseMessage

```

#### Implementation

##### prePrepare message processing

```typescript

public void onPrePrepare(PbftBaseMessage message) {

String key = message.getNo();

if (message.isSwitch()) {//if is block chain switch,remove the before proposal

logger.warn("block chain switch, again proposal block num: {}, data: {}",

message.getBlockNum(), message.getDataString());

remove(key);

}

if (preVotes.contains(key)) {

//The description has been initiated, can not be repeated, can only initiate a vote at the same

height

return;

}

preVotes.add(key);

//Start timeout control

timeOuts.put(key, System.currentTimeMillis());

//

checkPrepareMsgCache(key);

//Into the preparation phase, if not the sr node does not need to be prepared

if (!checkIsCanSendMsg(message)) {

return;

}

PbftBaseMessage paMessage = message.buildPrePareMessage();

forwardMessage(paMessage);

if (message.getType() == PBFT_SR_MSG) {

srPbftBaseMessage = message;

}

}

```

##### prepare message processing

```typescript

public void onPrepare(PbftBaseMessage message) {

String key = message.getKey();

if (!preVotes.contains(message.getNo())) {

//Must be prepared in advance

pareMsgCache.put(key, message);

return;

}

if (pareVotes.contains(key)) {

//Explain that the vote has been voted and cannot be repeated

return;

}

pareVotes.add(key);

//

checkCommitMsgCache(message.getNo());

if (!checkIsCanSendMsg(message)) {

return;

}

//The number of votes plus 1

if (!doneMsg.containsKey(message.getNo())) {

long agCou = agreePare.incrementAndGet(message.getDataKey());

if (agCou >= Param.getInstance().getAgreeNodeCount()) {

agreePare.remove(message.getDataKey());

//Entering the submission stage

PbftBaseMessage cmMessage = message.buildCommitMessage();

doneMsg.put(message.getNo(), cmMessage);

forwardMessage(cmMessage);

}

}

//Subsequent votes will definitely not be satisfied, timeout will be automatically cleared.

}

```

##### commit message processing

```typescript

public void onCommit(PbftBaseMessage message) {

String key = message.getKey();

if (!pareVotes.contains(key)) {

//Must be prepared

commitMsgCache.put(key, message);

return;

}

if (commitVotes.contains(key)) {

//Explain that the node has voted on the data and cannot vote repeatedly.

return;

}

commitVotes.add(key);

//The number of votes plus 1

long agCou = agreeCommit.incrementAndGet(message.getDataKey());

dataSignCache.getUnchecked(message.getDataKey())

.add(message.getPbftMessage().getRawData().getDataSign());

if (agCou >= Param.getInstance().getAgreeNodeCount()) {

remove(message.getNo());

//commit,

if (!isSyncing()) {

pbftMessageAction.action(message,

dataSignCache.getUnchecked(message.getDataKey()));

srPbftBaseMessage = null;

}

}

}

```

## References

1. [Practical Byzantine Fault Toleranceand Proactive Recovery](https://www.microsoft.com/en-us/research/wp-content/uploads/2017/01/p398-castro-bft-tocs.pdf)
2. [The latest gossip on BFT consensus](https://arxiv.org/pdf/1807.04938.pdf)
3. [Practical Byzantine Fault Tolerance](http://pmg.csail.mit.edu/papers/osdi99.pdf)
4. [Threshold signatures, multisignatures and blind signatures based on the gap-Diffie-Hellman-group signature scheme](https://link.springer.com/content/pdf/10.1007/3-540-362886_3.pdf)

