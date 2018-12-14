---
tip: 10
title: TRC-10 Token Standard
author: Marcus Zhao<zhaohong229@gmail.com>
type: Standards Track
category: TRC
status: in process
created: 2018-11-11
---
## Simple Summary

A standard interface for tokens.


## Abstract

The following standard allows for the implementation of a standard API for tokens on native chain. This standard provides basic functionality to transfer tokens.

## Motivation
A standard interface allows any language to implement the token.
## Specification

## Token
### Methods

**NOTES**:

#### ID
returns the id of token
#####
ID is integer stored as string and start from 100001. 
the ID less then 100000 is reserved.
#### name
#####
returns the name of token
When the ALLOW_SAME_TOKEN_NAME proposal is opened, duplicate names are allowed

#### symbol
returns the symbol of token.

#### presion
Returns the number of decimals the token uses - e.g. 6, means to divide the token amount by 1000000 to get its user representation.
#####
The value range is between 0 to 6.
ALLOW_SAME_TOKEN_NAME proposal needs to be turned on first. Otherwise, it defaults to 0

#### totalSupply
Returns the total token supply.

#### frozen_supply
the list of the amount and duration of frozen tokens 

#### trx_num
the equivalent TRX amount, for example：232241

#### num
the equivalent custom amount of assets

#### start_time
starting time, for example：20170312

#### end_time
finishing time, for example：20170512

#### description
Token description, for example：”trondada”

#### url
the URL link of the token. 

#### free_asset_net_limit
free available bandwidth for transferring this specific asset of each account. 

#### public_free_asset_net_limit
free available bandwidth for transferring this specific asset of all accounts. 

#### public_free_asset_net_usage
free bandwidth used by all acounts for transferring this specific asset. 

#### public_latest_free_net_time
the amount of time used on free bandwidth when the token was most recently transferred
