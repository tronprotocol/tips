``` 
tip: 28
title: TRC-28 Built-in message queue for event subscribe
author: jiangyy <jiangyangyang@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/28
status: Final
type: Standards Track
category: Informational
created: 2019-03-14
```

## Simple Summary
Adding built-in message queue for event subscribe in java-tron. 

## Abstract
The built-in message queue is designed for event subscribe. Developers could subscribe triggers directly from fullnode without event plugin.

## Motivation
Developers could use event plugins to subscribe triggers from fullnode, which provide very reliable service and store very large amount of data. 

But in some cases, developers want to subscribe directly from fullnode, with short-term subscriptions. Native message queue is implemented to meet such requirement.

## Specification
The function of native queue is configurable. It's is disabled by default. It shared the configuration of triggers with eventplugin.

The communication channel between fullnode and subscription client is socket. The bindport could be configurable to avoid conflicting.

event.subscribe = {
native = {
useNativeQueue = true // if true, use native message queue, else use event plugin.
bindport = 5555 // bind port
sendqueuelength = 1000 //max length of send queue
}
......
}

Developers should subscribe triggers very conveniently. What they need to do is: connecting to the port, subscribing the topics, then receivingthe triggers.
