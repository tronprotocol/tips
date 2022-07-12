```
tip: 17
title: Adaptive Energy Limit Model
author: nanfengpo <nanfengpo@hotmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/17
status: Final
type: Standards Track
category: TRC
created: 2018-12-29
```

## Simple Summary

This doc describes the  standard interface of the Adaptive Energy Limit Model


## Abstract

In the current TRON network, the creation and operation of smart contracts require Energy consumption. Energy can only be obtained by freezing TRX, the amount of Energy obtained = TRX/Total TRX * Total Energy Limit of the whole network for obtaining Energy frozen.   

For example, if the total amount of TRX frozen for Energy in the current network is 1_000_000_000 TRX, and an account with 1_000 TRX frozen accounts for one-millionth of the total amount frozen, then the Energy limit for that account is 32400 Energy.

However, if some accounts freeze TRX and have the corresponding energy, but do not use it, energy resources will be wasted. To this end, the Adaptive Energy Limit Model is proposed in this document. This model can automatically adjust the upper limit of energy according to the current energy consumption tension. Specifically,
- when energy consumption is low, increase the energy limit so that each account can get more energy
- when energy consumption is high, lower the energy ceiling so that each account has less energy

## Motivation

1. Avoid waste of energy resources;
2. Each account has more energy resources;

## Implementation

This model adjusts the energy owned by each account by adjusting the total upper limit of the total network energy. For the energy of the entire Tron network, there are the following measures:
- Real Energy Limit: An upper limit on the real capacity of the TRON network within 24 hours. The current value is 100 billion. This value can be modified by proposal.
- Virtual Energy Limit: An upper limit on the virtual capacity of the TRON network within 24 hours. Used to calculate the energy owned by an address in real-time, changes per block.The current maximum is 50 times the Real Energy Limit. The multiplier 50 can be adjusted by the proposal.
- Target Energy Limit: The target upper limit of Energy consumed in one minute (equal to 50% * RealEnergyLimit/(24 * 60)), used to measure whether the TotalEnergyAverageUsage in the past minute is small or large, so as to determine whether the virtual upper limit is high or low, that is, whether the network is congested or not.  The ratio 50%  can be adjusted by the proposal.[will change as the RealEnergyLimit changes]
- Average energy usage over the last minute: changes per block

Adjustment strategy:
The width of the sliding window is 1 minute. Calculate the average Energy usage in a window:
- increase the Virtual Energy Limit when the usage amount is greater than the Target Energy Limit within 1min. The increase is 1/1000. The maximum is increased to 50 times the Real Energy Limit
- if the usage amount is less than the Target Energy Limit within 1min, the Virtual Energy Limit will be reduced. The reduction is 1/100. The minimum is reduced to one times the Real Energy Limit  

For example, the initial Virtual Energy Limit is 500_000_000_000L and the target ceiling is 500_000_000L.
When the energy usage is <500_000_000 in the first minute, Virtual Energy Limit:= Virtual Energy Limit *1000/999 = 500_500_000_000. When the energy usage is >500_000_000 in the second minute, Virtual Energy Limit = Virtual Energy Limit *99/100=495_500_000_000. However, the Virtual Energy Limit is within the range of [Real Energy Limit, Real Energy Limit * 1000], that is, after the second minute, the Virtual Energy Limit is still 500_000_000_000



