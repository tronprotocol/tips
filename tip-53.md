```
tip: 53
title: Optimize the current TRON delegation mechanism
author: lvs007 <zy.liang.5@163.com>
discussions to: https://github.com/tronprotocol/TIPs/issues/53
category: TRC
status: Final
created: 2019-07-31
```
## Simple Summary
This doc describes a solution to optimize the current TRON delegation mechanism

## Abstract
At present, the TRON's delegation mechanism is that the user votes for the node. If the node is elected sr, then each block will reward sr with 32 TRX, and the top 100 votes will receive additional rewards; if the node does not give the user dividends, then users can not get rewards, it can not improve the enthusiasm of users to vote, resulting in a lower mortgage rate on the whole network.

## Motivation
Improve the mortgage rate of the entire network TRX, while increasing the user's income more fairly

## Specification
Two types of rewards: block reward and voting reward.
Block reward: the SR will get 16 TRX for each block it has generated.
Voting reward: for each block, the most-voted 127 SRs will receive TRX in proportion to the votes they get. Each block will reward 160 TRX in total, and each SR will get (SR’s votes/ total votes) * 160 TRX.
The rewarded TRX will not be added to the “allowance” field of the SR immediately. Users (including SRs) will have to withdraw TRX by themselves so that the rewards will show up on their account balance.
Meanwhile, SRs can take a percentage of commission from the dividends distributed to the users. For the commission, SRs can specify a value from 0 to 100. 0 means that no TRX will be extracted from users’ dividends, while 100 means that all dividends will be taken by the SRs. Also, SRs can modify the percentage and the new percentage will take effect from the next maintenance period.

### Current Situation

The current setting for block production rewards is 32 TRX per block. The block production cycle is 3 seconds. For every six hours, there will be two production cycles counting the votes without packing the blocks. Thus, the number of blocks packed by TRON blockchain is 86400 / 3 - 2 * 4 = 28792.
Thus, the daily rewards for block production are 32TRX/block * 28792 block = 921344 TRX.
The voting rewards are 16 TRX per block. So the daily voting rewards stands at 16TRX/block * 28800 block = 460800 TRX.

Such incentive mechanism encourages nodes to participate in the election of supernodes. By being a part of the production process and benefiting from it, the nodes have a stake in the game and keep the network runs smoothly. Those who didn't get elected would also receive voting rewards depending on the number of votes they got. The combination of production rewards and voting rewards takes all parties in the network into consideration and provides an enabling environment for nodes to contribute to the TRON network.

Let's look deeper into the on-chain data and the operation of TRON blockchain.
Currently, the volume of votes in the network is around 8.2 billion, taking up only less than 10% of the total number of votes. The reasons for such low participation, judging by the current operating parameters, is the low return rate. The daily voting rewards for each vote is 60672TRX / 8200000000 votes /day = 5.7584e-05 TRX/vote/day; the average annual return is 5.7584e-05 * 365 = 2.1%. Due to the unimpressive return rate, nodes that have TRX are not motivated to participate in the voting process.
From the perspective of block production rewards, the first 27 supernodes receive a total number of 7.5 billion votes. With the same formula, the daily block production rewards are 
921344TRX / 7500000000 votes / day = 1.2284e-04 TRX/vote/day, which means the annual rewards rate is about 1.2284e-04*365 = 4.4%.
The comparison shows that block production rewards are higher than voting rewards.

The other problem is that the first and the twenty-seventh nodes produce the same amount of blocks in one day. But the first supernode has a total of 520 million votes and an annual production rewards rate of 2.4%, the twenty-seventh supernode has 180 million votes and 6.9% production rewards rate. This data shows that the node with more votes is rewarded even less than those who have fewer votes, which creates an unfair situation.

Therefore, the incumbent incentive mechanism has the following three issues:
1. High threshold for participating in the election
Judging by the on-chain data, the 27th and the 28th candidate are 50 million votes apart. That's over 40% of the total votes of the 28th candidate. Because voting rewards is only half as much as the production rewards, the profit gained by the 28th candidate is significantly lower than that of the 27th candidate, which causes drastic competition for the slot of the 27th candidate. In order to keep its slot, the node that is elected as the 27th will try to safeguard its position and widen the gap between the 28th and itself.

2. Rewards distribution are not fully decentralized.
The current mechanism is to have both production rewards and voting rewards directly distributed to the nodes. This method can only achieve a certain level of decentralization instead of making the system fully decentralized, for the rewards cannot get to the individual voters. After the nodes obtain the rewards, they will distribute them to the voters. However, this process itself is centralized and out of the scope of blockchain management.

3. On-chain governance and incentive mechanism not separated
Under current mechanism, production reward is far higher than the voting reward. Those who are not able to take part in the on-chain governance have lost the interest and the will to contribute to the community, which in a way severs the connection between the government body and the entire community. In the long run, that will make TRON blockchain become a somewhat centralized ecosystem, dampening its long-term growth. Once a supernode is down, it will be hard to fill its place right away, undermining the efficiency of the network.

### Algorithm

Dividends SRs:

The starting cycle(current cycle) defaults to 0, and each time the maintenance period is changed, it is automatically incremented by 1 (that is, the current cycle is incremented by 1 for each maintenance period).
After the user votes, the node is rewarded from the next maintenance period, the reward period is a maintenance period, the reward is recalculated in the next maintenance period, the reward period is also a maintenance period, and so on.
Each block will give the generating block node and other sr dividends, give the generating block node 16TRX reward, and give the reward of the top 127 nodes 160TRX (according to the proportion of votes), one record per maintenance period for each node
The format is: <key, value>, key:cycle + "-" + address + "-reward"; value: the number of TRX rewarded.
In this way, the overall delegation mechanism dividend will be changed into a dividend for each block, which includes the 16TRX reward to the current generate block sr and 127 candidate sr nodes dividend 160TRX (the current generate block sr can get two dividends; other Candidate sr gets a bonus)

Dividends to users:

How to distribute dividends to users adopts active trigger mechanism: it is divided into three parts when the user re-votes when the user unfreezes when the user withdraws the reward
Calculation Rules:
Whether there is the last period (begin and end both exist and begin+1=end), if there is a need to calculate the dividends of this part, and calculate the current dividend from begin+1; if not, then from begin calculating the current dividends (this time you need to determine whether the current user's voting information is empty, if the empty setting is set begin=current+1, and return)
And re-recording the start cycle(begin) of the vote, and the end cycle: end=begin+1, and the current user vote information

New  block reword distribution plan:

The current block distribution plan is 32 TRX reword to SR who produce the block and 16 TRX reword equally distributed to SRs and stand-by SRs according to the voting number.
To encourage SRs to have more voters,  we will change the 32 TRX(reword to block producer) to 16TRX and 16TRX (reword to all SRs according to the voting number)  to 160 TRX.

## Rationale

### Advantages:

1. A decentralized dividend distribution mechanism featuring fairness that encourages 
greater user participation.  Moving the distribution process on the chain and keeping the record on the blockchain makes the rewards distribution completely decentralized and trackable.

2. Greater voter turnout and higher delegation rate, which vitalizes the community and 
strengthens the economic system across the network  

3. Fewer unnecessary dividend distribution transactions, leading to less bandwidth 
consumption and thus a more robust network 

4. The foundation for more complex consensus and incentive plans, signaling more 
possibilities and convenience for future development 


### Future goals:

#### A Brand New Consensus Mechanism

A new hybrid consensus mechanism has been running smoothly on TRON for 15 months. The stability of the DPOS consensus mechanism plays a significant part in this success, but we should also notice there is room for the DPOS mechanism to improve - for example, shorter block confirmation time and SPV support. 

Therefore, we plan on developing a new hybrid consensus mechanism based on DPOS+PBFT, under which the new automatic dividend distribution system will help to realize a new set of complex token dividend distribution rules. 

The new hybrid consensus mechanism will help to expand the scalability of the TRON ecosystem, unify cross-chain protocols and improve DApp usability.


#### Punishment Mechanism

TRON’s sound progress is closely related to the stable and efficient block generation of our excellent SR nodes. That being said, we have also noticed a relatively high block missing rate and low packaging rate in some nodes due to undesirable equipment and network performance. 

These nodes are slowing down the overall network speed, which can be harmful to the network and unfair to other SRs. To address this problem, we plan to introduce the automatic dividend distribution mechanism. By punishing unreliable and malicious nodes more directly, efficiently and accurately, the mechanism will be of great use in improving the performance of the whole network. 
	

####  Proposal Prize Pool

As of today, 26 proposals have been initiated in the TRON network, each contributing to the development of the network. Nevertheless, we believe that the proposals can help us achieve autonomy in the community to a greater extent. 

In order to encourage more community members to take part in the proposals, we plan to add a “prize pool” with an automatic dividend distribution scheme to the existing proposal mechanism. The prize pool will be created by each proposal initiator. SRs who actively participate in voting will receive incentives directly. 

Moving on, we will also innovate and modify the way we organize proposals, e.g. participant eligibility, initiator eligibility, participant number, etc., so as to improve community activity and lower the cost for an efficient community autonomy.

#### Giving Back To The Community
The new delegation mechanism and staking rewards distribution mechanism will be an important milestone in the evolution of our TRON protocol. Fair and transparent reward distribution mechanism will attract a wide range of nodes to participate in the TRON Blockchain network governance. At the same time, excluding the dividend payout transactions, the operation of the TRON Blockchain network will be more efficient.

In order to express our gratitude to all SRs for their outstanding contributions to TRON networks over the past year, TRON Foundation proposes a 50 million TRX distribution:

The detail of the distribution rule is:
SR(i) Reward = 50 millions * M(i) / N
M(i) = The amount of blocks SR(i) has produced till Oct 15, 2019
N = The number of blocks all the SRs (exclude the GRs) have produced till Oct 15,  2019

For example, one SR produce 100,000 blocks in this period and the total amount of blocks all SR produced is 20,000,000, then this SR can receive 50 million * 100,000 / 2,000,000 = 2.5 million TRX.

The proposal will be created on about Oct 15, 2019.  Only after the proposal is approved, so can the 50 million TRX distribution be executed.  

