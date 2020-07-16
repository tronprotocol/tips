```
tip:  64
title: tron mix consensus Analytics
author: xing@tron.network
status: Draft
type: algorithm
category : Core
created: 2019-12-17
```
## Simple Summary
This TIP mainly describes widely used pBFT and give some explanation how it works on tron consensus algorithm.
[Optimize pBFT](https://github.com/tronprotocol/tips/blob/master/tp/ticp/ticp-optimized-pbft/ticp-Optimized-PBFT.md)
## Abstract
Practical Byzantine Fault Tolerance(pBFT) is designed for reaching a consensus in the distributed network like blockchain even when some nodes in the network fail to response or controlled by hacker or response with wrong result. In order to fully implement pBFT, system need to configure a certain number of replicas. This TIP will give some simple proof of 3f+1 and 2f+1 based on precious research paper. In addition, give proof of correctness and performance of optimized tron consensus algorithm.
## Motivation 
In the distributed network, it is very hard for very node to keep status of other nodes and also ensure the correctness of data since instability networks environments. Any request can be delayed, or fail to send or manipulated by hackers like TCP hijacking , etc.  Reach a global consensus state between different nodes is interest topic and lots of scientists start to overcome this problem by coming up with different innovative architecture. pBFT is a really efficient way to solve it by providing 3f+1 replicas in the network.
## Specification
Normally, pBFT have `request->Pre-prepare->prepare->commit->reply`  five types of message, but optimized tron pBFT just have `Pre-prepare->prepare->commit` four types of message, which is much easier to manipulate and implement.  By combining with current tron consensus algorithm, the first phase is block broadcasting, which is equivalent to the pre_prepare phase of traditional PBFT; the second is the vote stage where blocks are verified, equivalent to the prepare phase of traditional PBFT; the third phase is verifying vote results, equivalent to the commit phase of traditional PBFT. Below are the details:
1. SRs will broadcast the message after producing a block
2. Upon receiving the broadcast block, Verifiers will validate it, then sign and broadcast the result
3. Upon receiving signed prepare messages from more than 2/3+1 Verifiers, a commit message will be generated, which will then be signed and broadcasted by Verifiers
4. If nodes receive signed commit messages from more than 2/3+1 Verifiers, it is deemed that the current block can never be reverted
Basically, by adding multiple Verifiers in the current tron network shorten the block confirmation time. Current tron consensuses algorithm always require 2f+1 =19 nodes to confirm block, which take 19 slot time, while optimized tron pBFT only require 2/3+1 verifiers to confirm blocker, which take less times in comparing with former since network request can be handled by few seconds.
Consider about slide windows model, Current tron consensus algorithm only move one slot every pass, while optimized tron pBFT can move multiple slot once receiver 2/3+1 Verifiers replies. Below is current tron consensus algorithm:
 ```
     Tron window:       start..........................End
      Block     A  ----> B->C...........17..........--->R                    (a)
      Status  solid ---> unconfirmed->...........->unconfirmed
 ```
Initially, slide window starts from the first unconfirmed block, the size is 1, then will increase windows size as the number of unconfirmed block increase. Once windows size reach threshold say 19+1, which is R in above, then make B‘s status to be solid, move into C, decrease windows size by one, which is 19.And continue to move once start point block of windows become solid status.
When combined with optimized tron pBFT, the windows can move faster.
```
 Tron window:     start....................................End
 optimized:       start                  end(receives message)              (b)
 Block     A  ----> B----->C------>D------>E..............--->R
 Status  solid ---> unconfirmed->...................->unconfirmed
```
For optimized PBFT, slide window starts from the first unconfirmed block with size of 1,  will increase windows size as the number of unconfirmed block increase when 2/3+1 relies message from verifiers not be received.  Once get more than 2/3+1 replies messages from verifiers stating that block E is valid, which proves that block E on (b) is valid, which draws a conclusion that B,C,D,E are all valid and can be marked as solid status since each block hash relies precious block hash . In this case, the slide windows move super faster in comparing with tron windows before tron windows reach thresholds-19.  In best case, which means no fork and network is good means a slot time is enough to receive Verifiers replicas, both of them have the same move speed after tron windows size reach threshold. However, if there is a fork on the main chain, then tron window (a) reset windows size and wait for 19 blocks time to confirm while optimized windows (b) can maintenance the same move speed. More detail: See the proof the correctness of optimized pBFT.
  
Notice: even if (a) and (b) have same window moving speed, the transaction confirm time of (a) is much bigger than (b) since it need to wait more than 2f+1 block to be produced to valid a block

## Rationale 
## Proof of 3f+1
Following will give some simple proof about pBFT. We denote
```
R=3f+1
```
where f is the maximum number of replicas that may be faulty, R is a set of replicas.  In an asynchronous system, R is optimal, namely it is the minimum number which can guarantee the correctness of data. 
- why??
 ``` n ``` is the number of replicas in the network. 
 f faulty replicas would send wrong data, while remaining n-f can rely correct data to client. However, it is possible that f replicas that did not response are no-faulty. In order to get correct data, we must ensure that n-2f>f, which is n>3f. Since n is an integer, so the minimum integer which satisfies this inequation is 3f+1. 
So, now we get n=3f+1.
 
## Proof of 2f+1  
   
 There are a total of 5 states between client and replicas in normal case operations: request, pre-prepare, prepare, commit, reply. The init state is request, the final state is reply. The convert sequence is as following:
 ```
   request->Pre-prepare->prepare->commit->reply
 ```
Firstly, the client send request to primary replicas, once primary replica receive request and it will start three-phase protocol and send multicast to all the replicas. Once other replicas receive valid Pre_prepare message , they will send multicast to all the replicas. In every state, once replicas receive request from precious state and then will send a multicast to the network after confirm message with correct view number and sequence number.
 Each state depends the precious state within same view message, like if commit is true , then both prepare and Pre-prepare should are true. If commit is true, there are at least f+1 no-faulty replicas in a set R1 send a request to this replica from prepare state within same view message m and also there are f+1 no-faulty replicas send a request from Pre_Prepare state within same view message m. However, there are can be some network failure which cause primary replica not receive request message from client. At this time, it trigger 'three-phase protocol ' change view, recreate a new primary replicas and increase view number to be v+1. Consider this case, any view v'>v contains correct view-change messages from every replica in a set R2 of 2f+1 replicas. Since there are  total 3f+ 1 replicas, R1 and R2 must intersect in at least one no faulty replica k. k’s view-change message will ensure that prepared in a previous view is propagated to subsequent views ,unless the new-view message contains a view-change message with a stable checkpoint with a sequence number higher than n. But this is impossible that no replicas in the new view accept message with sequence number lower than n.  
 ```
   |R2|-|R1|>=1
   |R2|+|R1|=3f+1          (1)     →|R2|>=2f+1
  Or 
   |R1|-|R2|>=1
   |R1|+|R2|=3f+1          (2)    → |R2|<=2f+1
 ```
  Combine (1) and (2),  |R2|=2f+1.  
  We denote Q is a set of replicas which is reponsed for confirm message during commit status like R2 or R1. |R| is a set of total replicas in the system.  In order to reach consensus, any two |Q| with |R| must intersect in at least one replica, the same as above proof. However, pBFT any time there can be max f fault replica or cheat nodes which was controlled by hacker, so the inequation would be like the following:
```
   2*Q -|R|>=1+f  -> Q>=(|R|+1+f)/2   → Q>=(4f+1+1)/2 → Q>=2f+1
```   
In consideration of both cases, so we need at least 2f+1 replicas to ensure the correctness of the result. More detail [check this paper](http://pmg.csail.mit.edu/papers/osdi99.pdf)
### Proof of Correctness of Optimized Tron pBFT
 `Assumption`: SR can successfully broadcast message to the network after finishing produce a block.  
 After SR finish producing block and broadcast message to all Verifiers, there might be some network failures happen, like network delay, package loss, etc. We denote that ` f1 ` is the max number Verifiers that would be faulty before receiving broadcast message , ` f2 ` is the max number of Verifiers that would be faulty after receive SR broadcast message. `f` is the max number of faulty Verifiers as we set by default. So, f>max(f1,f2). Based on pBFT, we should set total Verifiers :
```
3f2+1 <=3f+1
```
If f1 is zero, then 3f2+1=3f+1 since there is no any failure happen before receiving broadcast message. To successful verified correctness of result, we need:
```
2f2+1<=2f+1
```
The same as above , only if f1=0, then 2f2+1=2f+1.
When receive at least 2f+1 replies from Verifiers, then confirm block status can be solid status. 2f+1 always bigger or equal than 2f2+1. Worst case f1=f, then need all the remaining Verifiers that successful receive broadcast message from SR , which is 2f+1=3f2+1>2f2+1.  Best case, f1=0, just need at least 2f2+1=2f+1 Verifiers replies.  If f>f1>0, then 2f+1 >2f2+1 always true.  Therefore, keep at least 2f+1 replies from Verifiers always ensure the correctness of the result.
### Proof of Performance of Optimized Tron pBFT
However, if the network is not good, f1 increase, then it is hard to get 2f+1 replies from Verifiers, which mean this round fail to reach consensus for block A validation. But if the next block B or C successful reach consensus from Verifiers, then all the unconfirmed block before B or C on the main chain will also become a solid state since block B or C alway contain precious block hash and generations of hash depend precious block hash. So, this optimized tron pBFT would have a greater performance on average.
```
A-->B--->C--->D-->E.......
``` 
  case like A fails, B fail, C success is the same as the case like A success, B success, C success, which means fail will not degrade performance. In the worst case, if there is more than f+1 faulty Verifiers totally, then newly produced block can never be confirmed. But this contradicts our assumption, which would not happen in the real world.   
   Take block produce order and node received order into consideration. Below is block produce order:
 ```
    A-->B--->C--->D-->E.......      (1)
 ```
   Take a look node receive block order from Verifiers  (worst case below)
 ```
   E(fail)->D(fail)->C(fail)->B(fail)-A(success)  (1)
 ```
   Only success receive 2/3+1 Verifiers confirmation information for A, then at this time only valid A. But right now, there are four blocks fail to confirm, which all of their block confirmation messages should be supposed to arrive before A and get 2/3+1 Verifiers replies. What will happen next E or next round??
```
  A-->B--->C--->D-->E--->A1->B1->C1-->D1-->E1   (2)
```
   Next round, if still worst cases happen, then A->B->C->D->E->A1 would be valid and become solid blocks.  Denote m is max number of block replies information from Verifiers that receive in inverted order. Above example is 5 E->D->C->B->A. Give a number N=3f+1, which is total number of Verifiers in the network. So, m <N.  N SR will take turn to produce block, denote there is total S turns , which totally should produce total S*N blocks.  In the worst case, if above case repeat every round, so the average block confirm time is :(worst case m=N-1)
```
  S*N/((S*N/m-1)*m+1)=S*N/(S*N-m+1) = 1+(m-1)/(S*N-m+1)=O(1)
```
   There are total S*N blocks, take ((S*N/m-1)*m+1) slot time since current round received Verficiters message in inverted orders can confirm precious m block, there are total (S*N)/m rounds can confirm ((S*N/m-1)*m+1) blocks with last round one block plus precious totally  (S*N/m-1)*m blocks. 
   The upper bounder is constant, when S become infinity lim (m-1)/(S*N-m+1)=0. Consider small of S=1 and biggest m=N-1, then average confirm time would be 1+(N-2)/(N-1) closer to 2. But this still much better to 19, which is DPOS confirm slot time.  
   Again, look back block produce order and node receive block order. Block produce order as following: 
```
    A-->B--->C--->D-->E....... (2)
```
Node receive block order:
```
    E(fail)-->D(fail)--->C(success)--->B(fail)-->A(fail/success)....... (2)
```
 Comparing with case (1), this case always have better average confirmation time since one round it confirm more than one block while case 1 just confirm one block. Therefore, any cases like (2) ,which confirm more than one block in one round, have better confirm time.  
  
 
- fork  
 
  Rule 1: always choose the fork chain which first receive 2/3 +1 Verifiers replices as main chain. Rule 2 : if no any block receive 2/3 +1, then chose longer chain as the main chain. Follow order rule1->No->rule2.
  ```
                  -B---C---E.........->R   len=19
   main chain-A->            				 (3)
                  -D-->G-->S-->Z		   len=18
  ```
 
   Analysis of the performance of switch chain: Only when a node receive two blocks at the same time will open fork and store locally, two fork chain cannot always keep the same length based on rules. Worst case: the difference of the length of two fork chain is 1 block away. So, the confirm time would be almost twice as case (2). Still much better current tron consensus algorithm since it requires 19+18=37 slot time to confirm block and switch longer chain. 19 is the longer fork chain while 18 is shorter fork chain, so total slot time is 19+18=37. This case only confirm one block and switch chain.  
  ```
                  -B---C---E....->R->A->B...  len>=19+2=21
   main chain-A->            				        (4)
                  -D-->G-->S-->Z		            len=13
  ```
 
Take a look at optimized tron pBFT, consider cases like (3) though it is impossible, because one round produce period,there must be a node receive a 2/3 +1 replies. But if this case happen, both algorithms confirm only block which is B and choose correct main chain. let’s do some calculation for the probability of case 3 in optimized tron algorithm. Denote P1 is the probability of fail to receive ⅔+1 replies, which is 1/2 because nodes can successfully receive or fail to receive. So, the probability of (3) only successfully receive one block information from 2/3 +1 verifiers is (½)^37, which is a very small float number.Then let calculate the probability of a node receive inverted block produce order: based on current tron consensus algorithm, blocks are produced on different slot time and SR take turns to produce blocks, there are a total of 37 slots for case (3), each the probability of mismatch 1/2*X (0<=X<=1) if network is OK, then X=0,otherwise a mismatch would happen X=1. Still if we calculate the probability : (1/2)^37 since everyone is mismatch. There are total max 19! Sequences for fork chain 1, only one order is correct match order and also only one is inverted order. So the probability of inverted order would be 1/19!. However, this calculation requires every arrival have the same probability to go into different slots.  Still, if just consider about mismatch and successful arrival of 2/3 +1 verifiers messages , then the probability of case 3 is (1/2)^(37*2) * P , where P is the probability to get inverted order, it can be a pretty small number. 
  Back to case 4(worst case): the same analysis of case (3), but the difference is that next round will confirm precious 19-1=18 block plus current one. The average confirm time would closer to 1 as the length of chain grow. The same proof as case (2).
 
    Overall, Optimized tron pBFT have tremendously improve performance.
   

    