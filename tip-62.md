```
tip:  62
title: Tron consensus algorithm introduction
author: xing@tron.network
status: Draft
type: consensus algorithm
category : Core
created: 2019-12-18
 
```
 
## Simple Summary 
 
This TIP mainly describes tron consensus algorithm- Delegated Proof of Stake (DPoS) as well as gives some related concepts explanation.
## Abstract
 
DPoS , basically, it looks likes a voting system where account holders vote for a few delegates that will secure the network named Super Representative (SR) in tron.
 
## Motivation
 
Proof of Work POW, which is being used in bitcoin or ethereum,provides a good solution to resolve blockchain security problem. However, it consume too much power and compute resource since it need take lot of computations to get next block hash. In order to solve this problem, a light-weight DPoS had come to our eye in 2014, which was developed by Daniel Larimer,in 2014. Bitshares, Steem, Ark, and Lisk are some of the cryptocurrency projects that make use of DPoS consensus algorithm.
 
## Specification
 
### Epoch  
Every six hours is called Epoch in tron. In other words, a cycle for producing a certain number of blocks. 
### Slot   
Slot is a place where a newly produced block can be put into.  Once a block is successfully being produced, the system will assign a corresponding slot based on timestamp. A slot can be empty if fail to produce a block at a specific time.  
### Maintenance Period    
   Tron sets two slot time as maintenance period, which is used to calculate the number of votes each SR got as well as get the block producing order. Notice, there is no any producing or processing activities during maintenance period. Only get vote and get order.   
### Ballot  
  Tron defines that one TRX owns one ballot right, which can be used to vote for SRs selection. 
### Vote Process  
  Tron defines that vote for a SR candidate is a special deal, nodes can generate a vote transactions for voting SRs candidates.    


 
Tron implements DPoS algorithm in their own way. In each Epoch(every six hour), there are maintenance period and block producing period. The maintenance which take only 2 slot time is used for calculating votes and select top 27 SRs for next Epoch, while the block producing period is used for producing blocks. Each slot is 3 second, which also is a block producing time. 
 
## Rationale
There are a couple of stages in DPoS. 
1. Voting 
  - Firstly, those account holders who want to join in voting need to freeze their TRX . A vote power, bandwidth and energy can be received by freezed TRX.
  - Secondly, those account holders who freeze their account can vote SR candidates. After the end of the voting period, the top 27 SR candidates with highly number of votes can be a SR node, which can produce blocks.
2. Produce block 
  - check turn: On the last maintenance period, the top 27 SR would be elected and sorted by the number of votes they got. At the start of Epoch, System start to produce blocks based on current slot index % total SR 27. Once the SRs with least number of vote finish producing block, next round will start from the SR with highest number of votes to the SR with least number of votes and repeat until reach the end of Epoch. In addition, a slot index is used for located SR based on current linux producing time and latest block producing timestamp.
     ``` 
     Epoch:Epoch Start...............................Epoch End
    slot :  1     2    3 ..........................  119  120
    Status: block empty block .....................Maintain Period
    slot :  121    122    123 ................ .......  129  130
    Status: block block block .....................Maintain Period
    ```
  - validate transactions: Once SR get turn to produce block, it will validate all the transactions received from the network and then processing and packing them into blocks.
  - broadcast: After SR finish producing a block, it will broadcast a message to the network so that other SR knows produce status. 
   Notice: status can be fail since network failure may happen. If the SR failed to produce a block, then this produce slot will be empty and next SR will produce a new block follow the step 2 within his slot time.
3. Confirm 
  - the confirm process is based on the mechanism that later SRs produce new blocks which contain precious block hash inside header. when the first unconfirmed block has 2/3n+1=19 children blocks produced by different SRs, the first unconfirmed block will be entry confirmed status, also known as solid status.   
    ``` 
      block:  A --> B----->     ...18 new block....    ->R      
      status: solid->unconfirmed->....18 unconfirmed block->unconfirmed   
     ```
      After reach 19 unconfirmed block (excluding itself) after last solid block on main chain, then first unconfirmed block become solid block, namely confirm status. new status as following:

     ``` 
      block:  A --> B-----> C    ...17 block....    ->R ---->S     
      status: solid->solid->unconfirmed...17 unconfirmed block->unconfirmed->unconfirmed  
     ```
      Above mechanism is a little bit like sliding windows, the size of the window is 19+1 unconfirmed block, every time move one slot if corresponding SR successfully produce a block.

     ``` 
        window:          start..........................End  
        Block     A  ----> B->C...........17..........--->R
        Status  solid ---> unconfirmed->...........->unconfirmed
     ```
      Initially, slide window starts from the first unconfirmed block, the size is 1, then will increase windows size as the number of unconfirmed block increase. Once windows size reach threshold say 19+1, which is R in above, then will make B statue to be solid, move into C, decrease windows size by one, which is 19.
    

      
    Notice: if there is fork on main chain, the longer chain will be a main chain while the shorter fork chain will store locally in DB. Once  longest chain was confirmed, then local shorter chain will be invalid. 

    ```
                    -B---C---E.........->R
     main chain-A->
                    -D--G--S.......>S
    ``` 
    Firstly, tron alway chose longest chain main as main chain, like above chose A->B->C-E...._R.  If at specific time, length of two sub-chain is equal, like A-B-C vs A-D-S, then tron will chose first arrive block to process like B, so A->B-C->E can be main chain. Once block B was confirmed, then shorted chain A-D-G-S will be invalid.  

4. Reward 
  - vote reward: The top 127 candidates updated every round can share a huge number of TRX as mined. Those reward will be split in accordance with the vote weight each candidate receives. The account holder who joins in voting also receive reward from corresponding SR candidates.
  - block reward (SR reward): The top 27 candidates who are elected every round will share roughly 230,400 TRX as mined. The reward will be split evenly between the 27 SRs. On average, the SRs who produce a block will get 16 TRX. Once they successfully produce a block, the reward will immediately be sent to them.
 
  The optimized delegation mechanism will add dividend to both user and SRs, increase reward for top 127 SR candidates so that they have enough TRX to give back to vote users, which encourage more uses to join vote and boost community.  More details check [TIP-53](https://github.com/tronprotocol/tips/blob/master/tip-53.md)
 
  
  
  Tron consensus algorithm requires current unconfirmed block must have 2f+1 child block to confirm its status to be solid.  Why??  (will use PBFT 2f+1 rule)  
      
  The next block always contains previous block hash, so if first unconfirmed block is valid, then the next block is also valid since generation of next block hash based on previous block hash. Therefore, if first unconfirmed block is valid, then all its 2f+1 unconfirmed child block is also valid. In PBFT, it require 2f+1 no-faulty replicas to confirm correctness of result, which is the same as 2f+1 child block in tron network.
 
 
  

