---
tip: 35
title: TRC-35 rate limit of api traffic
author: shydesky<shydesky@gmail.com>
discussions-to: https://github.com/tronprotocol/TIPs/issues/51
status: Draft
type: Standards Track
category Interface
created: 2019-07-30
---  

## Simple Summary

This tip is about flow limit of the api interface. Limiting the api traffic is necessary to every node which usually has limited resources in the Tron Network.

## Abstract

The implementation of rate limit of api traffic is various, it can be implemented at the firewall level, at the web server level, or at the JVM level. This tip Limits the scope of the discussion to the JVM level.
There are many mature algorithms can be used, like Token bucket, Leaky bucket.

## Motivation

The reason limiting the api traffic is that node usually has limited resouces to support the api requests. A large number of requests in a short time can cause node out of service. We can guarantee the normal service of the node by limiting some api requests.

## Specification

The api request contains both http request and rpc request. So, we want to implement one general solution which can be used by these two type of api. So, the implementation is designed based on strategies. We can define different strategies to satisfy the different scenes and the strategies can be implemented by the user.
The control granularity is set at the specific interface.


## Rationale

The strategy is independent among the different api interfaces, so you can choose suitable strategy for every api interface. The default strategy of rate limit is also provided if you don't want define a specific strategy.

## Implementation

There are three types of strategy implemented in the java-tron right now. They are Global Preemptible Strategy, QpsStrategy, IPQPSStrategy. 
The Global Preemptible Strategy is implemented based on java semaphore. Every api request must require a permit before it is responded and release the permit after the response completes. 
The QpsStrategy and the IPQPSStrategy is implemented based on guava ratelimiter provided by Google. Every api request must require a resource and the number of resources is limited in one period.
