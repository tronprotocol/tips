## Abstract
This specification defines the Node Discovery protocol, a Kademlia-like DHT that stores information about Tron nodes. The Kademlia structure was chosen because it is an efficient way to organize a distributed index of nodes and yields a topology of low diameter.

## Definitions
### Node ID
Identity of a node, consists of 64 bytes. Each node has a unique ID.
### Node Distance
It is a logical distance, the `distance` between two node IDs is the bitwise exclusive or on the hashes of the IDs, taken as the number.
```
distance(n₁, n₂) = keccak256(n₁) XOR keccak256(n₂)
```
### Kademlia Table
Nodes in the Discovery Protocol keep information about other nodes in their neighborhood. Neighbor nodes are stored in a routing table consisting of 'k-buckets'. For each `0 ≤ i < 256`, every node keeps a k-bucket for nodes of distance between `2i` and `2i+1` from itself.

The Node Discovery Protocol uses `k = 16`, i.e. every k-bucket contains up to 16 node entries.

## Protocol

Node discovery messages are sent as UDP datagrams. Each message contains a `timestamp` field, is an absolute UNIX time stamp, used for message expiration check. Implementations should ignore any expired packets.

```typescript
message Endpoint {
  bytes address = 1;
  int32 port = 2;
  bytes nodeId = 3;
}
```

### Ping Packet (0x01)
```typescript
message Ping {
  Endpoint from = 1;
  Endpoint to = 2;
  int32 version = 3;
  int64 timestamp = 4;
}
```
`from` is the message sender. 

`to` is the message recipient. 

`version` is used to identify a P2P network. 

When a `Ping` packet is received, the recipient should reply with a `Pong` packet. It may also consider the sender for addition into the local table. Implementations should ignore any mismatches in version.

### Pong Packet (0x02)
```typescript
message Pong {
  Endpoint from = 1;
  int32 version = 2;
  int64 timestamp = 3;
}
```
`Pong` is the reply to `Ping`.

###  FindNeighbours Packet (0x03)
```typescript
message FindNeighbours {
  Endpoint from = 1;
  bytes targetId = 2;
  int64 timestamp = 3;
}
```
`targetId` consists of 64 bytes.

A `FindNeighbours` packet requests information about nodes close to `targetId`, When `FindNeighbours` is received, the recipient should reply with `Neighbors` packets containing the closest 16 nodes to `targetId` found in its local table.

###  Neighbors Packet (0x04)
```typescript
message Neighbours {
  Endpoint from = 1;
  repeated Endpoint neighbours = 2;
  int64 timestamp = 3;
}
```
`Neighbours` is the reply to `FindNeighbours`.

## Implements

### K-Bucket update

The k-bucket entries are sorted by the time last seen — least-recently seen node at the head, most-recently seen at the tail. Whenever a new node N₁ is encountered, it can be inserted into the corresponding bucket. If the bucket contains less than `k` entries N₁ can simply be added as the first entry. If the bucket already contains `k` entries, the least recently seen node in the bucket, N₂, needs to be revalidated by sending a Ping packet. If no reply is received from N₂ it is considered dead, removed and add N₁ to the front of the bucket.

### Recursive Lookup

A lookup locates the `k` closest nodes to a node ID.

The lookup initiator starts by picking `α` closest nodes to the target it knows of. The initiator then sends concurrent `FindNeighbours` packets to those nodes. `α` is a system-wide concurrency parameter, such as 3. In the recursive step, the initiator resends `FindNeighbours` to nodes it has learned about from previous queries. Of the `k` nodes the initiator has heard of closest to the target, it picks `α` that it has not yet queried and resends `FindNeighbours` to them. Nodes that fail to respond quickly are removed from consideration.

If a round of `FindNeighbours` queries fails to return a node any closer than the closest already seen, the initiator resends the find node to all of the `k` closest nodes it has not already queried. The lookup terminates when the initiator has queried and gotten responses from the `k` closest nodes it has seen.

```typescript
MAX_STEPS = 8;
ALPHA = 3;
 
public synchronized void discover(byte[] nodeId, int round, List<Node> prevTried) {
  if (round == MAX_STEPS) {
    return;
  }
  List<Node> closest = nodeManager.getTable().getClosestNodes(nodeId);
  List<Node> tried = new ArrayList<>();
  for (Node n : closest) {
    if (!tried.contains(n) && !prevTried.contains(n)) {
      nodeManager.getNodeHandler(n).sendFindNode(nodeId);
      tried.add(n);
      wait(50);
    }
    if (tried.size() == ALPHA) {
      break;
    }
  }
  if (tried.isEmpty()) {
    return;
  }
  tried.addAll(prevTried);
  discover(nodeId, round + 1, tried);
}
```
## Change Log
