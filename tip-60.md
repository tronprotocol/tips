```
tip: 60
title: TRC-60:Precompiled contract function for multi-signature verification
author: Sh11thead <ksl2945@gmail.com>
discussions to: https://github.com/tronprotocol/TIPs/issues/60
category: Core
status: Final
created: 2019-09-20
```

## Simple Summary
This doc describes a native TVM function which is used to validate multi-signature for a provided account.

## Abstract
TRON provided multiple signature functions allowing for permission grading, and each permission can correspond to multiple private keys. But in TVM, currently we only have `ecrecover()` function to verify single-signed message.But multiple-signed message can not be verified in TVM ,to solve this case,  we need a new function to support multiple-sign verification . 

## Motivation
Developer hope to validate multi-sign for account with specific permission in smart contracts.


## Specification

Add a new function named ***validatemultisign*** in solidity compiler .

This function could takes 4 parameters:

```
validatemultisign(
address accountAddress, // account address  
uint256 permissionId, //permissionId for account
bytes32 content, //content for verifying
bytes[] signatures//signatures to be verified
)
```

Pay special attention to the parameter `signatures`,
The specific signature method is implemented in java code as follows:
```
//parameters address，permissionId ，hash
byte[] address  = address
int permissionId = permissionId ;
byte[] hash= originData;

//merge
byte[] merged =  ByteUtil.merge(address,ByteArray.fromInt(permissionId),data);
//get the content to sign
byte[] toSign = Sha256Hash.hash(merged);


//sign content
List<Object> signs = new ArrayList<>();
signs.add(Hex.toHexString(key1.sign(toSign).toByteArray()));
signs.add(Hex.toHexString(key2.sign(toSign).toByteArray()));
```
This function will call to a specific address (for example,`0x000000000000000000000000000000000000000a`) which will executed precompiledContracts in TVM to validate multi-sign.Since in TRON, one transaction allow max up to 5 different account to sign,the parameter `signatures` is allow max up to 5.

In TVM , we could reuse `ECKey.ECDSASignature.fromComponents(r, s, v)`method,which is already used by `ecrecover()` to recover address for signature.
## Energy cost
energy charge for the execution cost 1500 per signature

## Rationale
This function allows validating multi-sign in TVM could improve smart contract access to TRON blockchain which is good for both DApp developer and users.

## Backwards Compatibility

Adding a new precompiledContract cause no backwards compatibility concerns.

## Test Cases

1.Verifying both correct and incorrect signatures in smart contract.
2.Verifying duplicate signatures.
3.Verifying more than 5 signatures.
