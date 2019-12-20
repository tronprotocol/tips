```
tip:  61
title: Tron consensus algorithm introduction
author: xing@tron.network
discussions-to: <URL>
status: Draft
type: Core
category : Core 
created: 2019-12-18

```

## Simple Summary  

This TIP mainly describes tron consensus algorithm- Delegated Proof of Stake (DPoS) as well as give some basic introduction about related algorithms like PBFT, which was implemented on tron block validation. 

## Abstract 

 DPoS , basically, it looks likes a voting system where account holders vote for a few delegates that will secure the network named Super Node (SR) in tron. Practical Byzantine Fault Tolerance-PBFT is widely used in distributing environment so as to safeguard against the system failures like network delay , nodes dead ,attack ,etc. 

## Motivation 

Proof of Work POW, which is being used in bitcoin or ethereum,provide a good solution to resolve blockchain security problem. However, it consume too much power and compute resource since it need take lot of computation to get next block hash. In order to solve this problem, a light-weight DPoS had come to our eye in 2014, which was developed by Daniel Larimer,in 2014. Bitshares, Steem, Ark, and Lisk are some of the cryptocurrency projects that make use of DPoS consensus algorithm. 

## Specification 

Tron implements DPoS algorithm in their own way. Like there are 27 Super node total, which dynamically elected by account holders every 6 hours. 

## Rationale 
There are a couple of stages in DPoS.  
1. Voting  
   - Firstly, those account holders who want to join in voting need to freeze their accounts. The reason why we need freezing is that avoid race conditions.  
   - Secondly, those account holders who freeze their account can vote SR candidates. After the end of voting period, the top 27 SR candidates with highly number of votes can be a SR node, which can product a new block.
2. Produce block  
   - check turn: tron use round-robin algorithm to decide which SR is responsible for producing block based on currentTime, latest block time and the number of active witness node on the network.
   - validate transactions: Once SR get turn to produce block, it will validate all the transactions it receiver from the network and then processing and packing them into blocks. 
   - broadcast: After SR finish producing a block, it will broadcast a message to the network so that other SR knows produce status.  
    Notice: status can be fail since network failure may happen. If SR fail to produce a block, the network will reset the state and begin next round voting and do the same process until research success status. 
3. Confirm  
   - Once producing block SR receive 2/3+1 replies from other SR, then this block is being confirmed by the whole network.  Why ?? Take a look at PBFT section.
4. Reward  
   - vote reward: The top 127 candidates updated every round can share 115,200 TRX as mined. Those reward will be split in accordance with the vote weight each candidate receives. The account holder who joins in voting also receive reward from corresponding SR candidates.
   - block reward (SR reward): The top 27 candidates who are elected every round will share roughly 230,400 TRX as mined. The reward will be split evenly between the 27 SRs. On average, the SRs who produce a block will get 16 TRX. 
   
   The optimized delegation mechanism will add dividend to both user and SRs, increase reward for top 127 SR candidates so that they have enough TRX to give back to vote users, which encourage more uses to join vote and boost community.  More details check [TIP-53](https://github.com/tronprotocol/tips/blob/master/tip-53.md)
      
 
    

## PBFT   

   Roughly give an introduction based on tron consensus algorithm. We denote  
   ``` 
   R=3f+1
   ```  
where f is the maximum number of replicas that may be faulty, R is a set of replicas.  In the asynchronous system, R is optimal, namely it is the minimum number which can guarantee the correctness  of data.    
- why??  

    ``` n ``` is the number of replicas in the network.    
    f replicas would send wrong data, while remaining n-f can rely correct data to client. However, it is possible that f replicas that did not response are faulty. Therefore, total max replicas that would be faulty are 2f. In order to get correct data, we must ensure that n-2f>f, which is n>3f. Since n is an integer, so the minimum integer which satisfies this inequation is 3f+1.  In the simple send and reply model (only two state), when client successfully receive f+1 replies then it can said yes to this result.  
    So, now we get n=3f+1.   
    However, there are total 5 states between client and replicas in normal case operations: request, pre-prepare, prepare, commit, reply. The init state is request, the final state is reply. The convert sequence is like following:
    ``` 
      request->Pre-prepare->prepare->commit->reply 
    ```
    Firstly, the client send multicast to all the replicas, once primary replica receive request and then will send multicast to all the replicas. Once other replicas receive Pre_prepare message, they will send multicast to all the replicas. In every state, once replicas receive request and then send a multicase to the network after confirm.   

    Each status depend the precious status, like if commit is true , then prepare and Pre-prepare are all true. In prepare status, if a replica confirm status is true, which means there are at least f+1 no-faulty replicas send a request to this replica. This is local confirm, also refer as prepare_out. if prepare_out is true ,  commit_in must be true since each status has in and out and in status depend last out status. Move into commit status, if commit_in is true, then at least f+1 no-faulty replicas which match prepare_out status  (true), at least 2f+1 no-faulty replicas which math Pre-prepare_out status.   


    So this could be an interesting probability problem, but this tip do not talk deeply about proof of 2f+1. More detail [check this paper](http://pmg.csail.mit.edu/papers/osdi99.pdf)

