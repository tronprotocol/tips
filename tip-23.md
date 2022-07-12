```
tip: 23
title: TRC-23 Add the account world status tree root to the block header
author: lvs007 <liangzhiyan@tron.network>
discussions to: https://github.com/tronprotocol/TIPs/issues/23
status: Final
type: Standards Track
category: TRC
created: 2019-03-04
```

## Simple Summary

The purpose is to verify the consistency of the entire account.

## Abstract

Now it's hard to compare the consistency of each account database, so add the account world status tree root to the block header. The purpose is to verify the consistency of the entire account.

## Motivation

## Specification

modify the block header structure, add the accountStateRoot
```message BlockHeader{
 message raw
 	{int64 timestamp = 1;
 		bytes txTrieRoot = 2;
 		bytes parentHash = 3;
 //bytes nonce = 5;
 //bytes difficulty = 6;
 		int64 number = 7;
 		int64 witness_id = 8;
 		bytes witness_address = 9;
 		int32 version = 10;
 		bytes accountStateRoot = 11;
 	}
 	raw raw_data = 1;
 	bytes witness_signature = 2;
 }
```

###Account State Root Generate
Introduced the Ethereum's world state tree model
At a certain height, the block node starts to generate the root of the account status tree, and then adds the root to the block header. The subsequent block will generate a new account status tree with the account status tree in the previous block header as the root.
The nodes of other blocks will generate a new world state tree root according to the transactions in the block, and compare whether the generated root is consistent with the root in the current block header.

###Account State Root Validate
If the local account state and the account state of the block are inconsistent when the block is synchronized, a Bad Block exception will be thrown.