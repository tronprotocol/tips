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

#### symbol
returns the symbol of token.
#### decimals
Returns the number of decimals the token uses - e.g. 8, means to divide the token amount by 100000000 to get its user representation.
#####
The value range is between 0 to 6.

#### totalSupply
Returns the total token supply.
#### balanceOf
Returns the balance of account.
#### transfer

### Events

#### Transfer

#### Approval

## Implementation
