```
tip:  62
title: Tron consensus algorithm introduction
author: xing@tron.network
status: Draft
type: algorithm
category : Core
created: 2019-12-18
 
```
 
## Simple Summary 
 
This TIP mainly describes tron consensus algorithm- Delegated Proof of Stake (DPoS) as well as gives some related concepts explanation.
## Abstract
 
DPoS , basically, it looks likes a voting system where account holders vote for a few delegates that will secure the network named Super Representative (SR) in tron.
 
## Motivation
 
Proof of Work POW, which is being used in bitcoin or ethereum,provides a good solution to resolve blockchain security problems. However, it consumes too much power and computes resources since it needs to take a lot of computations to get the next block hash. In order to solve this problem, a light-weight DPoS came to our eye in 2014, which was developed by Daniel Larimer,in 2014. Bitshares, Steem, Ark, and Lisk are some of the cryptocurrency projects that make use of DPoS consensus algorithm.
 
## Specification
 
### Epoch 
   Every six hours is called Epoch in tron. In other words, a cycle for producing a certain number of blocks.
### Slot 
  Slot is a place where a newly produced block can be put into.  Once a block is successfully being produced, the system will assign a corresponding slot based on timestamp. A slot can be empty if you fail to produce a block at a specific time. 
### Maintenance Period  
  Tron sets two slot time as maintenance period, which is used to calculate the number of votes each SR got as well as get the block producing order. Notice, there is no producing or processing activities during the maintenance period. Only get votes and get orders.  
### Ballot 
  Tron defines that one TRX owns one ballot right, which can be used to vote for SRs selection.
### Vote Process
  Tron defines that voting for a SR candidate is a special deal, nodes can generate a vote transaction for voting SRs candidates. 
 
 
Tron implements DPoS algorithm in their own way. In each Epoch(every six hour), include a maintenance period and block producing period. The maintenance which takes only 2 slot time is used for calculating votes and select top 27 SRs for next round, while the block producing period is used for producing blocks. Each slot is 3 second, which also is a block producing time. 
 
## Rationale
There are a couple of stages in DPoS. 
1. Voting 
  - Firstly, those account holders who want to join in voting need to freeze their TRX . A vote power, bandwidth and energy can be received by freezed TRX.
  - Secondly, those account holders who freeze their account can vote for SR candidates. After the end of the voting period, the top 27 SR candidates with a high number of votes can be a SR node, which can produce blocks.
2. Produce block 
  - check turn: On the last maintenance period, the top 27 SR would be elected and sorted by the number of votes they got. At the start of Epoch, System starts to produce blocks based on the current slot index % total SR 27. Once the SRs with the least number of votes finish producing blocks, the next round will start from the SR with the highest number of votes to the SR with least number of votes and repeat until reach the end of Epoch. In addition, a slot index is used for located SR based on current linux producing time and latest block producing timestamp.
   ```
    Epoch:Epoch Start...............................Epoch End
    slot :  1     2    3 ..........................  119  120
    Status: block empty block .....................Maintain Period
    slot :  121    122    123 ................ .......  129  130
    Status: block block block .....................Maintain Period
   ```
 
  - validate transactions: Once SR gets turn to produce block, it will validate all the transactions received from the network and then processing and packing them into blocks.
  - broadcast: After SR finishes producing a block, it will broadcast a message to the network so that other SR knows how to produce status. 
   Notice: status can be fail since network failure may happen. If the SR failed to produce a block, then this produce slot will be empty and next SR will produce a new block following step 2 within his slot time.
3. Confirm 
  - the confirm process is based on the mechanism that later SRs produce new blocks which contain precious block hash inside header. When the first unconfirmed block has 2/3n+1=19 children blocks produced by different SRs, the first unconfirmed block will be entry confirmed status, also known as solid status.   
    ```
    block:  A --> B----->     ...18 new blocks....    ->R     
    status: solid->unconfirmed->....18 unconfirmed block->unconfirmed   
    ```
    After reaching 19 unconfirmed blocks (excluding itself) after the last solid block on the main chain, then the first unconfirmed block becomes a solid block, namely confirm status. new status as following:
    ```
     block:  A --> B-----> C    ...17 block....    ->R ---->S    
     status: solid->solid->unconfirmed...17 unconfirmed block->unconfirmed->unconfirmed 
    ```
    Above mechanism is a little bit like sliding windows, the size of the window is 19+1 unconfirmed block, every time move one slot if corresponding SR successfully produces a block.
    ```
       window:          start..........................End 
       Block     A  ----> B->C...........17..........--->R
       Status  solid ---> unconfirmed->...........->unconfirmed
    ```
    Initially, the slide window starts from the first unconfirmed block, the size is 1, then will increase window size as the number of unconfirmed blocks increase. Once windows size reach threshold say 19+1, which is R in above, then will make B status to be solid, move into C, decrease windows size by one, which is 19.
    
   Notice: if there is a fork on the main chain, the longer chain will be a main chain while the shorter fork chain will store locally in DB. Once the longest chain is confirmed, then the local shorter chain will be invalid.
 
   ```
                   -B---C---E.........->R
    main chain-A->
                   -D--G--S.......>S
   ```
   Firstly, tron alway chose the longest chain main as the main chain, like above chose A->B->C-E...._R.  If at a specific time, length of two sub-chain is equal, like A-B-C vs A-D-S, then tron will choose the first arrival block to process like B, so A->B-C->E can be the main chain. Once block B was confirmed, then shorted chain A-D-G-S will be invalid. 
 
4. Reward 
  - vote reward: The top 127 candidates updated every round can share a huge number of TRX as mined. Those rewards will be split in accordance with the vote weight each candidate receives. The account holder who joins in voting also receives a reward from corresponding SR candidates.
  - block reward (SR reward): The top 27 candidates who are elected every round will share roughly 230,400 TRX as mined. The reward will be split evenly between the 27 SRs. On average, the SRs who produce a block will get 16 TRX. Once they successfully produce a block, the reward will immediately be sent to them.
 
  The optimized delegation mechanism will add dividend to both users and SRs, increase reward for top 127 SR candidates so that they have enough TRX to give back to vote users, which encourage more uses to join vote and boost community.  More details check [TIP-53](https://github.com/tronprotocol/tips/blob/master/tip-53.md)
 

 
 
  

