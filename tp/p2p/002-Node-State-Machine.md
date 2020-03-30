## Abstract
This document explains different node states and how nodes switch between states.

## Definitions

### Discovered
`Discovered` is the initial state wherein the local node will send a [Ping message](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#ping-packet-0x01) to the node in this state. A node will be initialized to `Discovered` state in the following cases:
1.  When start a node, its seed node will be initialized to `Discovered` state
2.  When start a node, the nodes which was saved from the last run of [Node Discovery protocol](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md) will be initialized to `Discovered` state   
3.  If a node has no information saved locally or is in `Nonactive` or `Dead` state when a [Ping message](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#ping-packet-0x01) is received, it will be initialized to `Discovered` state
4.  The new nodes carried by [Neighbours messages](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#neighbors-packet-0x04) will be initialized to `Discovered` state

### Dead
`Dead` means the node is offline and unable to communicate. A node will switch from `Discovered` to `Dead` state if it fails to ping.

### Alive
`Alive` indicates that node is online and able to communicate with others. A node will switch from `Discovered` to `Alive` state if it pings successfully. The node will then switch from `Alive` to `Active` state if it is successfully written into K-Bucket.

### Active
`Active` means the node has been written into [K-Bucket](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#kademlia-table) and is participating in [Node Discovery protocol](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md). A node will have its state set to `Active` in the following two cases:
1.  A node will switch from `Alive` to `Active` state if it is successfully written into [K-Bucket](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#kademlia-table)
2.  A node will switch from `Evictcandidate` to `Active` state if it pings successfully
    

### Evictcandidate
`Evictcandidate` is a temporary state. When a node in `Alive` state attempts to be written into [K-Bucket](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#kademlia-table) but at this time the corresponding bucket is full, it will challenge the node with the earliest update time in the bucket. The challenged node will switch to `Evictcandidate` state and the local node will send a [Ping message](https://github.com/tronprotocol/tips/blob/master/tp/p2p/001-Node-Discover-Protocol.md#ping-packet-0x01) to the node in this state.

### Nonactive
`Nonactive` means the node is offline. A node will switch from `Evictcandidate` to `Nonactive` state if it fails to ping.

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
