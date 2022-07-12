## Abstract
This document explains the scoring policy for neighbouring nodes. Node score is used for determining the priority level to establish connections. The higher the score , the higher the priority.

## Definitions

### Scoring metrics

####  Packet loss rate
Packet loss rate indicates the quality of data communication between nodes. The lower the rate is, the better the data communication will be.

#### Net latency
Net latency reflects the quality of network between nodes. The shorter the net latency is, the better the network quality will be.

####  TCP traffic
TCP traffic indicates how active it is between nodes. The bigger the TCP traffic is, the more active the communication between nodes will be.

#### Disconnection count
The number of disconnections between nodes shows their stability. The less frequent the disconnection is, the more stable the nodes will be.

#### Handshake
Nodes that had successful handshakes will be connected first because they have the same blockchain information with the local node.

### Penalty state
Nodes in the state of penalty have a score of 0, and won’t receive score for any other metrics.
Usually, these nodes
1.  disconnected less than 60 seconds ago
2.  are on the badNodes list 
3.  have inconsistent blockchain information

## Implements
It needs to be determined whether the node is in penalty state when calculating the score of the node. The node will have a score of 0 if it is in this state; otherwise, its score is the sum of all metrics.

The implementation code is demonstrated as below.
```typescript
public int getReputation() {
  if (isReputationPenalized()) {
    return 0;
  }
  return getPacketLossRateScore() + getNetLatencyScore() + getTcpFlowScore() + getDisconnectionScore() + getHandshakeScore();
}
```
### Packet Loss Rate Score
Packet Loss Rate Score is inversely proportional to packet loss rate. The score ranges from 0 to 100.
```typescript
private int getPacketLossRateScore() {
  MessageStatistics s = nodeStatistics.messageStatistics;
  long in = s.discoverInPong.getTotalCount() + s.discoverInNeighbours.getTotalCount();
  long out = s.discoverOutPing.getTotalCount() + s.discoverOutFindNode.getTotalCount();
  return out == 0 ? 0 : 100 - min((int) ((1 - (double) in / out) * 200), 100);
}
```
### Net Latency Score
Net Latency Score is inversely proportional to average net latency. The score ranges from 0 to 20.
```typescript
private int getNetLatencyScore() {
  return (int) (nodeStatistics.discoverMessageLatency.getAvrg() == 0 ? 0
      : min(1000 / nodeStatistics.discoverMessageLatency.getAvrg(), 20));
}
```
### TCP Traffic Score
TCP Traffic Score is directly proportional to TCP traffic. The score ranges from 0 to 20.
```typescript
private int getTcpFlowScore() {
  return (int) min(nodeStatistics.tcpFlow.getTotalCount() / 10240, 20);
}
```
### Disconnection Score
Disconnection Score is a negative number directly proportional to the number of disconnections and is ten times the Disconnection count.
```typescript
private int getDisconnectionScore() {
  return -10 * nodeStatistics.getDisconnectTimes();
}
```
### Handshake Score
Handshake Score is either 20, if there is at least 1 successful Handshake, or 0, if there is none.
```typescript
private int getHandshakeScore() {
  return nodeStatistics.p2pHandShake.getTotalCount() > 0 ? 20 : 0;
}
```
## Change Log
