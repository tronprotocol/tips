```
tip: 51
title: TRC-51 rate limit of API traffic
author: shydesky<shydesky@gmail.com>
discussions-to: https://github.com/tronprotocol/TIPs/issues/51
status: Final
type: Standards Track
category: Interface
created: 2019-07-30
```

## Simple Summary

This tip is about the flow limit of the API interface. Limiting the API traffic is necessary to every node which usually has limited resources in the Tron Network.

## Abstract

The implementation of the rate limit of API traffic is various, it can be implemented at the firewall level, at the webserver level, or at the API level. This tip Limits the scope of the discussion to the JVM level.
There are many mature algorithms can be used, like Token bucket, Leaky bucket.

## Motivation

The reason limiting the API traffic is that node usually has limited resources to support the API requests. A large number of requests in a short time can cause node out of service. We can guarantee the normal service of the node by limiting some API requests.

## Specification

The API request contains both the HTTP request and RPC request. So, we want to implement one general solution which can be used by these two types of API. So, the implementation is designed based on strategies. We can define different strategies to satisfy the different scenes and the strategies can be implemented by the user.
The control granularity is set at the specific interface.


## Rationale

The strategy is independent among the different API interfaces, so you can choose a suitable strategy for every API interface. The default strategy of rate limit is also provided if you don't want to define a specific strategy.

## Implementation

There are three types of strategies implemented in the java-Tron right now. They are Global Preemptible Strategy, QpsStrategy, IPQPSStrategy. 
The Global Preemptible Strategy is implemented based on java semaphore. Every API request must require a permit before it is responded and release the permit after the response completes. 
The QpsStrategy and the IPQPSStrategy are implemented based on guava rate limiter provided by Google. Every API request must require a resource and the number of resources is limited in one period.
