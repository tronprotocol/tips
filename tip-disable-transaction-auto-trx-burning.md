```
TIP: 
Title: Optimize TRX burning mechanism in transaction.
Author: Dmytro Shalaiev (shalaevdmitriy99@gmail.com)
Type: Standards Track
Category: Core
Created: 2023-04-13
```

## Simple Summary
This Tron Proposal describes methods for turning off TRX burn mechanism if resources not enough for transaction. This should improve UX and more accurate predicting of transaction costs.

## Abstract
Currently, TRON uses a resource consumption model which is advanced described here in documentation https://developers.tron.network/docs/resource-model#bandwidth-points-consumption

## Motivation
One of the main ways of TRON usage is payment processing, whether it is native TPX or other assets. In this industry, it is very important to have a predictable transaction cost. The problem that we faced is that when there are no available resources on the account, to cover them, TRX will burn. This is not always a convenient approach. For example, we have an account to which the user deposits his assets (tokens) and TRX, to pay these tokens out we use a preliminary delegation of resources(BP and ENERGY if needed*) to this account (which is described in Staking 2.0), but due to resources price fluctuations or inaccuracies in the calculations of delegated resources amount, it may happen that the deficiency is covered by the user's TRX, which would like to save and not use, and even worse is when its amount will ultimately not be enough to successfully complete the transaction.

So it will be cool in such situation 'mark' transaction that it should use only available resources (FREE/STAKED/DELEGATED) without existing TRX balance, it is not enough avaliable - REVERT.

## Specification

Add `disable_trx_burn?: boolean type` property to TX data object, that will indicate - Can available TPX be used for burning to cover transaction resource shortage.
If transaction 'marked' as `disable_trx_burn` and avaliable resources not enought for covering costs - REVERT tx in a standard manner.


## Rationale
Adding just one property simplifies the implementation for backward compatibility with the current transaction DTO because it can be optional if needed. And realization not changing the current resource consumption model at all, only disabling the 'last' step to obtain resources - burn TRX.
