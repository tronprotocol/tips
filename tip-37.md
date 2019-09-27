```
tip: 37
title: TRC-37: forbid using TransferContract & TransferAssetContract  for contract account
author: Taihao Fu <taihao.fu@gmail.com>
discussions to: https://github.com/tronprotocol/TIPs/issues/37
category: TRC
status: Final
created: 2019-05-10
```


## Abstract
Forbidding transfer trx/trc10 to a contract account can avoid the misunderstanding of the transfer transaction would executing fallback function in smart contract.

Also avoid user misuse system transfer contract to send their asset to a contract and asset would probably be locked in a contract forever.

## Motivation
Several report from our community shows dApp developer try to execute fallback function when use transferContract to send trx to their smart contract. But in our origin design it should not touch TVM. So, one option to resolve the misunderstanding is a hard fork to forbid the transaction to a smart contract address.  

## Specification
Add validate address logic in validate() function in TransferContract & TransferAssetContract. When the toAddress account type is Contract, throw a contract validate exception.

## Rationale
TransferContract & TransferAssetContract should only use bandwidth and not touch TVM. The two types of system contract would be better only for asset easy transferring on tron-network. 

For contract , user should trigger fallback function in the specific contract for trx/trc10 token transferring purpose.

## Backwards Compatibility
1. If old contract not implement fallback function in their contract, there would be no other way any more to send trx/trc10 to this contract.

2. tronlink or similar wallet should support a new transfer method to use bandwidth/energy to send trx/trc10 to the contract.

3. dApp developer may need to change their migration script/ dApp script a little bit for contract asset injection. 

4. tronweb should do the similar change for contract asset injection.
