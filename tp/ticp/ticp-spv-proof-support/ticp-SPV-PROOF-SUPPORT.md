```
ticp: 1
title: SPV proof support
author: @lvs007
type: Tron Inter-blockchain Communication Protocol
category: CORE
status: Draft
created: 2020-03-09
```

## Summary

This doc describes a solution to support SPV proof

## Abstract

This standard defines a way to support SPV correctness and security, In this way client can get certified block headers. The client can use transactions' Merkel root in headers to make a Merkel proof



## Motivation

Support more powerful features such as IBC in the future

## Specification

In DPOS consensus every slot is assigned to the only legal SR, So within one schedule if verifiers know the legal SR list they can verify every block header easily. Since verifiers don't process most transaction including vote transaction. they have no way to know the voting result. In other words they are unable to know the next legal SR list. The focus of this problem is how to handle the maintenance period correctly.
Based on the above reasons we can solve this problem by recording SR list in one type of BPFT messages which are sent by the previous legal SR list we trust. The PBFT information is in here #39

## Algorithm

We can use threshold signature to reduce the signature size. The new data struct includes the next SR list and a threshold signature signed by more than 2/3 SRs. This new data struct will record in the block headers of the next schedule's SRs. Verifiers can check this data to determine the new SR list is legal or not.

## Proto

```SrList

message SrList {
message raw {
bytes currentSrList = 1;
bytes nextSrList = 2;
}
bytes sr_signature = 3;
}


