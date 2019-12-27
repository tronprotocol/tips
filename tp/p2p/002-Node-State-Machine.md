## Abstract
This document explains different node states and how nodes switch between states.

## Definitions

### DISCOVERED
DISCOVERED is the initial state wherein the local node will send a Ping message to the node in this state. A node will be initialized to DISCOVERED state in the following cases:
1.  When start a node, its seed node will be initialized to DISCOVERED state
2.  When start a node, the nodes which was saved from the last run of Node Discovery protocol will be initialized to DISCOVERED state   
3.  If a node has no information saved locally or is in NONACTIVE or DEAD state when a Ping message is received, it will be initialized to DISCOVERED state
4.  The new nodes carried by neighbours messages will be initialized to DISCOVERED state

### DEAD
DEAD means the node is offline and unable to communicate. A node will switch from DISCOVERED to DEAD state if it fails to ping.

### ALIVE
ALIVE indicates that node is online and able to communicate with others. A node will switch from DISCOVERED to ALIVE state if it pings successfully. The node will then switch from ALIVE to ACTIVE state if it is successfully written into K-Bucket.

### ACTIVE
ACTIVE means the node has been written into K-Bucket and is participating in Node Discovery Protocol. A node will have its state set to ACTIVE in the following two cases:
1.  A node will switch from ALIVE to ACTIVE state if it is successfully written into K-Bucket
2.  A node will switch from EVICTCANDIDATE to ACTIVE state if it pings successfully
    

### EVICTCANDIDATE
EVICTCANDIDATE is a temporary state. When a node in ALIVE state attempts to be written into K-Bucket but at this time the corresponding bucket is full, it will challenge the node with the earliest update time in the bucket. The challenged node will switch to EVICTCANDIDATE state and the local node will send a Ping message to the node in this state.

### NONACTIVE
NONACTIVE means the node is offline. A node will switch from EVICTCANDIDATE to NONACTIVE state if it fails to ping.

## Implements
Here is the function for switching node states:
```typescript
public void changeState(State newState) {
  State oldState = state;
  if (newState == State.DISCOVERED) {
    sendPing();
  }
  if (!node.isDiscoveryNode()) {
    if (newState == State.ALIVE) {
	  Node evictCandidate = nodeManager.getTable().addNode(**this**.node);
	  if (evictCandidate == null) {
	    newState = State.ACTIVE;
      } else {
        NodeHandler evictHandler = nodeManager.getNodeHandler(evictCandidate);
        if (evictHandler.state != State.EVICTCANDIDATE) {
          evictHandler.challengeWith(this);
        }
      }
    }
    if (newState == State.ACTIVE && oldState == State.ALIVE) {
      nodeManager.getTable().addNode(node);
    }
    if (newState == State.NONACTIVE && oldState == State.EVICTCANDIDATE) {
      nodeManager.getTable().dropNode(node);
      replaceCandidate.changeState(State.ACTIVE);
    }
  }
  if (newState == State.EVICTCANDIDATE) {
    sendPing();
  }
  state = newState;
}
```
## Change Log
