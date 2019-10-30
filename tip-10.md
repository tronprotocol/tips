```
tip: 10
title: TRC-10 Token Standard
author: Marcus Zhao<zhaohong229@gmail.com>
type: Standards Track
category: TRC
discussion-to: https://github.com/tronprotocol/TIPs/issues/10
status: Final
created: 2018-11-11
```

## Simple Summary

A standard interface for tokens.


## Abstract

The following standard allows for the implementation of a standard API for tokens on the native chain. This standard provides basic functionality to transfer tokens.

## Motivation
A standard interface allows any language to implement the token.
## Specification

### Token
https://github.com/tronprotocol/protocol/blob/6138aa7ac3af751ee778259a140d3484f8d9e5a4/core/Tron.proto#L70
#### asset_issued_ID
returns the id of token
#####
The ID is integer stored as a string and start from 100001. 
the ID less then 100000 is reserved.
#### asset_issued_name
#####
returns the name of token
When the ALLOW_SAME_TOKEN_NAME proposal is opened, duplicate names are allowed

#### decimals
Returns the number of decimals the token uses - e.g. 6, means to divide the token amount by 1000000 to get its user representation.
#####
The value range is between 0 to 6.
ALLOW_SAME_TOKEN_NAME proposal needs to be turned on first. Otherwise, it defaults to 0

#### totalSupply
Returns the total token supply.

#### frozen_supply
the list of the amount and duration of frozen tokens 

#### trx_num
the equivalent TRX amount, for example,232241

#### num
the equivalent custom amount of assets

#### start_time
starting time, for example,20170312

#### end_time
finishing time, for example,20170512

#### description
Token description, for example,”trondada”

#### URL
the URL link of the token. 

#### free_asset_net_limit
The free available bandwidth for transferring this specific asset of each account. 

#### public_free_asset_net_limit
The free available bandwidth for transferring this specific asset of all accounts. 

#### public_free_asset_net_usage
free bandwidth used by all accounts for transferring this specific asset. 

#### public_latest_free_net_time
the amount of time used on free bandwidth when the token was most recently transferred

### The influences of the proposal AllowSameTokenName
The identity of the token will be id instead of name and every token will support decimal places after the proposal is approved, so it will affect the following structure and contracts.

```
message Account {
  // the other asset owned by this account, deprecated
  map<string, int64> asset = 6;
  // the other asset owned by this account, key is assetId
  map<string, int64> assetV2 = 56;

  // name of asset issued, deprecated
  bytes asset_issued_name = 17;
  // id of asset issued
  bytes asset_issued_ID = 57;

  // latest asset operation time, deprecated
  map<string, int64> latest_asset_operation_time = 18;
  // latest asset operation time, key is assetId
  map<string, int64> latest_asset_operation_timeV2 = 58;

  // free asset net usage, deprecated
  map<string, int64> free_asset_net_usage = 20;
  // free asset net usage, key is assetId
  map<string, int64> free_asset_net_usageV2 = 59;
}

AssetIssueContract: add field precision, means the number of decimal places

message TransferAssetContract {
  bytes asset_name = 1; // this field is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id which should be in string format.
  bytes owner_address = 2;
  bytes to_address = 3;
  int64 amount = 4; // the number of tokens in smallest unit
}

message ParticipateAssetIssueContract {
  bytes owner_address = 1;
  bytes to_address = 2;
  bytes asset_name = 3; // this field is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id which should be in string format.
  int64 amount = 4; // the amount of sun
}
**notice**
asset_name is token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise it is token id which should be in string format.

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
first_token_id and second_token_id are token name before the proposal ALLOW_SAME_TOKEN_NAME is active, otherwise they are token id in string format. first_token_balance and second_token_balance are the number of token in smallest unit. quant and expected are the number of token in smallest unit.
``` 
