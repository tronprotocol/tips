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

#### ID
returns the id of token
#####
ID is integer stored as string and start from 100001. 
the ID less then 100000 is reserved.
#### name
#####
returns the name of token
When the ALLOW_SAME_TOKEN_NAME proposal is opened, duplicate names are allowed

#### abbr
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

## API
message AssetIssueContract {
  message FrozenSupply {
    int64 frozen_amount = 1;
    int64 frozen_days = 2;
  }
  bytes owner_address = 1;
  bytes name = 2;
  bytes abbr = 3;
  int64 total_supply = 4;
  repeated FrozenSupply frozen_supply = 5;
  int32 trx_num = 6;
  int32 precision = 7;
  int32 num = 8;
  int64 start_time = 9;
  int64 end_time = 10;
  bytes description = 20;
  bytes url = 21;
  int64 free_asset_net_limit = 22;
  int64 public_free_asset_net_limit = 23;
  int64 public_free_asset_net_usage = 24;
  int64 public_latest_free_net_time = 25;
}
**notice**
asset_name is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id and token is should be in string format.

message ParticipateAssetIssueContract {
  bytes owner_address = 1;
  bytes to_address = 2;
  bytes asset_name = 3; // this field is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id and token is should be in string format.
  int64 amount = 4; // the amount of sun
}
**notice**
asset_name is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id and token is should be in string format.

message ExchangeCreateContract {
  bytes owner_address = 1;
  bytes first_token_id = 2;
  int64 first_token_balance = 3;
  bytes second_token_id = 4;
  int64 second_token_balance = 5;
}

message ExchangeInjectContract {
  bytes owner_address = 1;
  int64 exchange_id = 2;
  bytes token_id = 3;
  int64 quant = 4;
}

message ExchangeWithdrawContract {
  bytes owner_address = 1;
  int64 exchange_id = 2;
  bytes token_id = 3;
  int64 quant = 4;
}

message ExchangeTransactionContract {
  bytes owner_address = 1;
  int64 exchange_id = 2;
  bytes token_id = 3;
  int64 quant = 4;
  int64 expected = 5;
}

**notice**
token_id is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id and token is should be in string format.