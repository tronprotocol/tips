 
```
tip:  64
title: pBFT introduction
author: xing@tron.network
status: Draft
type: algorithm
category : Core
created: 2019-12-17
```
 
## Simple Summary
This TIP mainly describes widely used pBFT and give some explanation how it works on tron consensus algorithm.
 
 
## Abstract
Practical Byzantine Fault Tolerance(pBFT) is designed for reaching a consensus in the distributed network like blockchain even when some nodes in the network fail to response or controlled by hacker or response with wrong result. In order to fully implement pBFT, system need to configure a certain number of replicas. This TIP will give some simple proof of 3f+1 and 2f+1 based on precious research paper.
 
## Motivation  
In the distributed network, it is very hard for very node to keep status of other nodes and also ensure the correctness of data since instability networks environments. Any request can be delayed, or fail to send or manipulated by hackers like TCP hijacking , etc.  Reach a global consensus state between different nodes is interest topic and lots of scientists start to overcome this problem by coming up with different innovative architecture. pBFT is a really efficient way to solve it by providing 3f+1 replicas in the network.
 
 
## Specification 
 
Normally, pBFT have `request->Pre-prepare->prepare->commit->reply`  five types of message, but optimized tron pBFT just have `Pre-prepare->prepare->commit` three types of message, which is much easier to manipulate and implement.  By combining with current tron consensus algorithm, the first phase is block broadcasting, which is equivalent to the pre_prepare phase of traditional PBFT; the second is the vote stage where blocks are verified, equivalent to the prepare phase of traditional PBFT; the third phase is verifying vote results, equivalent to the commit phase of traditional PBFT. Below are the details:
 
1. SRs will broadcast the message after producing a block
 
2. Upon receiving the broadcast block, Verifiers will validate it, then sign and broadcast the result
 
3. Upon receiving signed prepare messages from more than 2/3+1 Verifiers, a commit message will be generated, which will then be signed and broadcasted by Verifiers
 
4. If nodes receive signed commit messages from more than 2/3+1 Verifiers, it is deemed that the current block can never be reverted
 Basically, by adding multiple Verifiers in the current tron network shorten the block confirmation time. Current tron consensuses algorithm always require 2f+1 =19 nodes to confirm block, which take 19 slot time, while optimized tron pBFT only require 2/3+1 verifiers to confirm blocker, which take less times in comparing with former since network request can be handled by few seconds. 
 
Consider about slide windows model, Current tron consensus algorithm only move one slot every pass, while optimized tron pBFT can move multiple slot once receiver 2/3+1 Verifiers replies. Below is current tron consensus algorithm:
 
   ```
       window:          start..........................End 
       Block     A  ----> B->C...........17..........--->R
       Status  solid ---> unconfirmed->...........->unconfirmed
    ```
 Initially, slide window starts from the first unconfirmed block, the size is 1, then will increase windows size as the number of unconfirmed block increase. Once windows size reach threshold say 19+1, which is R in above, then will make B statue to be solid, move into C, decrease windows size by one, which is 19. 
 
 When combined with optimized tron pBFT, the windows can move faster.
 
 ```
  window:          start....................................End 
  optimized:       start                  end(receives message)
  Block     A  ----> B----->C------>D------>E..............--->R
  Status  solid ---> unconfirmed->...................->unconfirmed
 ```
 Initially, slide window starts from the first unconfirmed block, the size is 1, then will increase windows size as the number of unconfirmed block increase and do not receiver 2/3+1 relies message from verifiers.  Once receive 2/3+1 replies messages from verifiers , which show that block E is valid, then B,C,D,E are all valid and be marked as solid status since each block hash relies precious block hash . At this cases, the slide windows move super faster in comparing with tron windows.
 
 
## Rationale  
## Proof of 3f+1 
 
Following will give some simple proof about pBFT. We denote
 ```
 R=3f+1
 ```
where f is the maximum number of replicas that may be faulty, R is a set of replicas.  In an asynchronous system, R is optimal, namely it is the minimum number which can guarantee the correctness of data.  
- why??
  ``` n ``` is the number of replicas in the network.  
  f replicas would send wrong data, while remaining n-f can rely correct data to client. However, it is possible that f replicas that did not response are faulty. Therefore, total max replicas that would be faulty are 2f. In order to get correct data, we must ensure that n-2f>f, which is n>3f. Since n is an integer, so the minimum integer which satisfies this inequation is 3f+1.  In the simple send and reply model (only two state), when client successfully receive f+1 replies  then it can said yes to this result.
  So, now we get n=3f+1. 
 
 
## Proof of 2f+1
 
  There are total 5 states between client and replicas in normal case operations: request, pre-prepare, prepare, commit, reply. The init state is request, the final state is reply. The convert sequence is like following:
  ```
    request->Pre-prepare->prepare->commit->reply
  ```
  Firstly, the client send multicast to all the replicas, once primary replica receive request and then will send multicast to all the replicas. Once other replicas receive Pre_prepare message, they will send multicast to all the replicas. In every state, once replicas receive request from precious state and then send a multicast to the network after confirm. 
  Each state depend the precious state within same view message, like if commit is true , then prepare and Pre-prepare are all true. If commit is true, there are at least f+1 no-faulty replicas in a set R1 send a request to this replica from prepare state within same view message m and also there are f+1 no-faulty replicas send a request from Pre_Prepare state within same view message m. However, there are can be some network failure which cause primary replica not receive request message from client. At this time, it trigger 'three-phase protocol ' change view, recreate a new primary replicas and increase view number to be v+1. Consider this cases, any view v'>v contains correct view-change messages from every replica in a set R2 of 2f+1 replicas. Since there are 3f+ 1 replicas, R1 and R2 must intersect in at least one no faulty replica k. k’s view-change message will ensure that prepared in a previous view is propagated to subsequent views ,unless the new-view message contains a view-change message with a stable checkpoint with a sequence number higher than n. But this is impossible that no any replicas in the new view accept message with sequence number lower than n.
 
  In consideration of both cases, so we need at least
  ```
  max(f+1,2f+1)=2f+1
  ```
 replicas to ensure the correctness of result in distributed network. No one can ensure that primary replica always works, so view changes will happen. 
 
  So this could be an interesting probability problem, but this tip do not talk deeply about proof of 2f+1. More detail [check this paper](http://pmg.csail.mit.edu/papers/osdi99.pdf)
 
 
  ### Proof of Correctness of Optimized Tron pBFT
  `Assumption`: SR can successfully broadcast message to the network after finishing produce a block.  
 
  After SR finish producing block and broadcast message to all Verifiers, before Verifiers receive this message, there might be some network failure happen, like network delay, package loss, etc. We denote that ` f1 ` is the max number Verifiers that would be faulty from SR broadcast state to Verifiers received state, ` f2 ` is the max number the max number Verifiers that would be faulty after receive SR broadcast message. `f` is the max number the max faulty Verifiers as we set by default. So, f>max(f1,f2). Based on pBFT, we should set total Verifiers :
 
```
 3f2+1 <=3f+1
```
 If f1 is zero, then 3f2+1=3f+1 since there is no any failure happen from SR broadcast message state to Verifiers received state. To successful verified correctness of result, we need:
```
 2f2+1<=2f+1
```
 The same as above , only if f1=0, then 2f2+1=2f+1.
 When receive at least 2f+1 replies from Verifiers, then confirm block status to be solid. 2f+1 always bigger or equal than 2f2+1. Worst case f1=f, then need all the Verifiers that successful receive broadcast message from SR replies, which is 2f+1=3f2+1>2f2+1.  Best case, f1=0, just need at least 2f2+1=2f+1 Verifiers replies.  If f>f1>0, then 2f+1 >2f2+1 always true.  Therefore, keep at least 2f+1 replies from Verifiers always ensure the correctness of the result.
 
 However, if the network is not good, f1 increase, then it is hard to get 2f+1 replies from Verifiers, which mean this round fail to reach consensus for block A validation. But if the next block B or C successful reach consensus from Verifiers, then all the unconfirmed block before B or C on the main chain will also become a solid state since block B or C alway contain precious block hash and generations of hash depend precious block hash. So, this optimized tron pBFT would have a greater performance on average.
 ```
 A-->B--->C--->D-->E.......
 ```
  case like A fails, B fail, C success is the same as the case like A success, B success, C success, which means fail will not degrade performance.
 

