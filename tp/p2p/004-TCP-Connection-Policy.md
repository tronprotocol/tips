## Abstract
This document introduces the TCP connection policy, including methods to select neighboring nodes and to process a TCP connection request.

## Definitions

### Node Types

#### `activeNodes`
Specify through configuration file. Upon initiation, system will add `activeNodes` into `trustNodes` and try to build connections with them. If the connection with `activeNodes` fails, a retry will be launched in the next TCP cycle.

#### `trustNodes` 
Specify through configuration file. System will skip all other verifying steps and create a connection right away upon receiving a request from `trustNodes`. More details refer to [Processing TCP connection requests](#processing-tcp-connection-requests).

#### `badNodes`
When receiving an abnormal message, system will add the sender node into `badNodes` and keep its status for 1 hour. The connection requests from `badNodes` will be directly rejected.

#### `recentlyDisconnectedNodes`
When a connection is broken, the node will be added to `recentlyDisconnectedNodes` for 30 seconds. To improve P2P connection quality, the connection requests from `recentlyDisconnectedNodes` will be directly rejected to avoid establishing bad links.

### Node Scores
The node scoring function calculates the score of a node based on many metrics. Higher scores indicate higher priority to establish a connection.

### Connection Parameters

#### `maxNodes` 
Maximum number of TCP connections. Requests to connect when reaching `maxNodes` will be rejected directly.

####  `minNodes` 
Minimum number of TCP connections. Nodes with fewer connections than `minNodes` will actively establish connections with other nodes.

####  `minActiveNodes` 
Minimum number of TCP connections that initiate requests. Nodes will actively establish connections with other nodes if there are fewer request-sending connections than `minActiveNodes`. This is to prevent malicious nodes taking up all connections.

####  `maxNodesWithSameIp` 
Maximum TCP connections for an IP. This parameter will limit the connections one set of nodes can establish with the same node, so as to prevent potential attacks when all connections for one node is taken up by one.

## Implements

### Steps to establish TCP connection

Upon the establishment of TCP connection, a polling will take place among nodes in every 3.6 seconds. The working process is demonstrated below.

step 1: Add the unconnected `activeNodes` to `connectNodes`.
```typescript
List<NodeHandler> connectNodes = new ArrayList<>();
Set<String> nodesInUse = new HashSet<>();

channelManager.getPeers().forEach(channel -> {
 nodesInUse.add(channel.getPeerId());
});

channelManager.getActiveNodes().forEach((address, node) -> {
 if (!nodesInUse.contains(node.getHexId())) {
   connectNodes.add(nodeManager.getNodeHandler(node));
   nodesInUse.add(node.getHexId());
 }
});
```

step 2: Calculate the number of remaining `lackSize` connections.
```typescript
int size = Math.max(minActiveNodes - peers.size(), minActiveNodes - activePeers.get()));
int lackSize = size - connectNodes.size();
```

step 3: Select `lackSize` nodes and add them to `connectNodes`. First, select the eligible nodes from the list of neighboring nodes, then select `lackSize` nodes with the highest score.
```typescript
public List<NodeHandler> getNodes(Predicate<NodeHandler> predicate, int limit) { 
  List<NodeHandler> filtered = new ArrayList<>(); 
  for (NodeHandler handler : nodeHandlerMap.values()) { 
    if (handler.getNode().isConnectible() && predicate.test(handler)) { 
      filtered.add(handler); 
    }
  } 
  filtered.sort(Comparator.comparingInt(handler -> -handler.getNodeStatistics().getReputation())); 
  return CollectionUtils.truncate(filtered, limit); 
}
```

Adopt the filtering strategy, and filter out the following nodes during selection.
1. self node
2. node already connected to
3. node recorded in the `recentlyDisconnectedNodes` list
4. node recorded in the `badNodes` list
5. node with established ip connections reaching the maximum `maxNodesWithSameIp`
```typescript
public boolean test(NodeHandler handler) { 
  InetAddress inetAddress = handler.getInetSocketAddress().getAddress(); 
  return !((handler.getNode().getHost().equals(nodeManager.getPublicHomeNode().getHost()) && handler.getNode().getPort() == nodeManager.getPublicHomeNode().getPort()) 
    || (channelManager.getRecentlyDisconnected().getIfPresent(inetAddress) != null) 
    || (channelManager.getBadPeers().getIfPresent(inetAddress) != null) 
    || (channelManager.getConnectionNum(inetAddress) >= maxNodesWithSameIp) 
    || (nodesInUse.contains(handler.getNode().getHexId())) 
    || (nodeHandlerCache.getIfPresent(handler) != null)); 
}
```

step 4: Establish TCP connection with `connectNodes` and cache the nodes for 3 minutes as filtering purposes. namely, the node won't be automatically connected for 3 minutes to prevent occurrences of invalid connections.
```typescript
connectNodes.forEach(n -> {
  peerClient.connectAsync(n, false);
  nodeHandlerCache.put(n, System.currentTimeMillis());
});
```

#### Processing TCP connection requests

Upon receiving a TCP connection request, the following receiving conditions will be checked.
 1. Decide whether the node is trust node; if the answer is no, the node should be further determined, and will be denied the request if meeting any of the following conditions.
	 - reaching the maximum connections
	 - in the `recentlyDisconnectedNodes` list
	 - in the `badNodes` list
	 - having established `maxNodesWithSameIp` connections with the same IP
  
 2. Decide whether the connection is repeated connection; if the answer is yes, disconnect the one later established.
```typescript
public synchronized boolean processPeer(Channel peer) { 
  if (trustNodes.getIfPresent(peer.getInetAddress()) == null) { 
    if (recentlyDisconnected.getIfPresent(peer) != null) { 
      return false; 
    } 
    if (badPeers.getIfPresent(peer) != null) { 
      peer.disconnect(peer.getNodeStatistics().getDisconnectReason()); 
      return false; 
    } 
    if (!peer.isActive() && peers.size() >= maxNodes) { 
      peer.disconnect(TOO_MANY_PEERS); 
      return false; 
    } 
    if (getConnectionNum(peer.getInetAddress()) >= maxNodesWithSameIp) { 
      peer.disconnect(TOO_MANY_PEERS_WITH_SAME_IP); 
      return false; 
    } 
  } 
  Channel channel = peers.get(peer.getNodeIdWrapper()); 
  if (channel != null) { 
    if (channel.getStartTime() > peer.getStartTime()) { 
      channel.disconnect(DUPLICATE_PEER); 
    } else { 
      peer.disconnect(DUPLICATE_PEER); 
      return false; 
    } 
  } 
  peers.put(peer.getNodeIdWrapper(), peer); 
  return true; 
}
```
