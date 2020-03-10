---
```
tip: xx 
title: Zero-knowledeg Proof Verification Instructions 
author: federico<federico.zhen@tron.network>
discussions-to: https://github.com/tronprotocol/tips/issues/xx
status: draft
type: Standards Track
category: TRC
created: 2020-03-09
```

## Simple Summary 

The TIP provides the zero-knowledge proof verification instructions in shielded contract, which can be used in shielded token transactions.

## Abstract 

The TIP introduces three new instructions: `VERIFYMINTPROOF`, `VERIFYTRANSFERPROOF`, and `VERIFYBURNPROOF`, which can accelerate the zero-knowledge verification for the `mint`, `transfer` and `burn` modules in shielded token contract. 

## Motivation 

In order to implement shielded transaction for [TRC-20](https://github.com/tronprotocol/TIPs/blob/master/tip-20.md) token,  We have developed the shielded token contract. The contract has three core modules: `mint`, `transfer` and `burn`. `mint` is used to transform the public TRC-20 tokens into shielded tokens. `transfer` is used for shielded  token transactions. `burn` is  used to transform the shielded  tokens back to public TRC-20 tokens.  The shielded contract is implemented based on zero-knowledge proof, so it needs the complex zero-knowledge proof verification in `mint`, `transfer` and `burn` methods. In order to accelerate the speed, we will make use of  instructions in the contract to implement the verification process. 

## Specification

(1)`VERIFYMINTPROOF` 

`VERIFYMINTPROOF` is used to verify the validity of zero-knowledge proof when transforming the public TRC-20 token into shielded tokens.  

```
(bool result,bytes memory msg) = VERIFYMINTPROOF(byte[1480] intput);
```

The length of `input` is 1480 bytes. For the output, `reuslt` is a bool value to indicate whether the proof verification succeeds, the length of `msg` is 33~1057 bytes, which returns the node value to construct the Merkle tree. The time cost of `VERIFYMINTPROOF` instruction takes about 10ms.

（2）`VERIFYTRANSFERPROOF` 

`VERIFYTRANSFERPROOF` is used to verify the validity of zero-knowledge proof for shielded tokens transactions.  

```
(bool result,bytes memory msg) = VERIFYTRANSFERPROOF(byte[2144] intput);
```

The length of `input` is 2144 bytes. For the output, `reuslt` is a bool value to indicate whether the proof verification succeeds, the length of `msg` is 66~1058 bytes, which returns the node value to construct the Merkle tree. The time cost of `VERIFYTRANSFERPROOF` instruction takes about 15ms in parallel mode.

（3）`VERIFYBURNPROOF`指令 

`VERIFYMINTPROOF` is used to verify the validity of zero-knowledge proof when transforming the shielded tokens back to  public TRC-20 tokens.  

```
(bool result,bytes memory msg) = VERIFYBURNPROOF(byte[488] input);
```

The length of `input` is 488 bytes. For the output, `reuslt` is a bool value to indicate whether the proof verification succeeds, the length of `msg` is 0. The time cost of `VERIFYBURNPROOF` instruction takes about 10ms.

## Rationale

By introducing the zero-knowledge proof verification instructions, it will be more convenient for shielded token contract implementation, which can providing users stronger privacy for shielded token transactions.

## Test Cases



## Implementation 



