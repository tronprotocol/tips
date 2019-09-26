```
tip: 32
title: TRC-32 Clear the ABI of contract
author: llwslc<llwslc@gmail.com> 
discussions to: https://github.com/tronprotocol/TIPs/issues/32
category: TRC
status: Final
created: 2019-4-3
```

## Abstract

This TIP specifies a new api, which clears the ABI of contract.

## Motivation

The contract does not need ABI anymore after the introduction of triggerConstantContract api.

## Specification

A new api, `clearContractABI`, is introduced.

`// api.proto
 rpc ClearContractABI (ClearABIContract) returns (TransactionExtention) {}
 
 // Contract.proto
 message ClearABIContract {
   bytes owner_address = 1;
   bytes contract_address = 2;
 }
 
 // Tron.proto
 ClearABIContract = 47;`
 
The `clearContractABI` parameters are shown as follows:
`clearContractABI contract_address`
Http interface example:
Step 1. Call api: wallet/clearabi to build the transaction
`curl -X POST  http://127.0.0.1:8090/wallet/clearabi -d '{"owner_address": "415A523B449890854C8FC460AB602DF9F31FE4293F","contract_address": "416162AFF58D27A5FBD15B2F8F7EF752B2F4256086"}'`
Return:
`{"visible":false,"txID":"b33337e74de5ca8f6155003b588ae8a4d6580432d41a86d9086a244fb2960ab2","raw_data":{"contract":[{"parameter":{"value":{"owner_address":"415a523b449890854c8fc460ab602df9f31fe4293f","contract_address":"416162aff58d27a5fbd15b2f8f7ef752b2f4256086"},"type_url":"type.googleapis.com/protocol.ClearABIContract"},"type":"ClearABIContract"}],"ref_block_bytes":"0c19","ref_block_hash":"4b4f1264c3f9d924","expiration":1558685682000,"timestamp":1558685622423},"raw_data_hex":"0a020c1922084b4f1264c3f9d92440d092a0c7ae2d5a630830125f0a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e436c656172414249436f6e7472616374122e0a15415a523b449890854c8fc460ab602df9f31fe4293f1215416162aff58d27a5fbd15b2f8f7ef752b2f42560867097c19cc7ae2d"}`
Step 2. Call api: wallet/gettransactionsign to sign (use the private key of the transparent address)
`curl -X POST  http://127.0.0.1:8090/wallet/gettransactionsign -d '{"privateKey":"","transaction":{"visible":false,"txID":"b33337e74de5ca8f6155003b588ae8a4d6580432d41a86d9086a244fb2960ab2","raw_data":{"contract":[{"parameter":{"value":{"owner_address":"415a523b449890854c8fc460ab602df9f31fe4293f","contract_address":"416162aff58d27a5fbd15b2f8f7ef752b2f4256086"},"type_url":"type.googleapis.com/protocol.ClearABIContract"},"type":"ClearABIContract"}],"ref_block_bytes":"0c19","ref_block_hash":"4b4f1264c3f9d924","expiration":1558685682000,"timestamp":1558685622423},"raw_data_hex":"0a020c1922084b4f1264c3f9d92440d092a0c7ae2d5a630830125f0a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e436c656172414249436f6e7472616374122e0a15415a523b449890854c8fc460ab602df9f31fe4293f1215416162aff58d27a5fbd15b2f8f7ef752b2f42560867097c19cc7ae2d"}}'`
Return:
`{"visible":false,"signature":["0e7e750226f01096f2f4aa0c2d03ad17d7ff57277ac3b655ecd692e3d9bd9bb822426dc779f046d79eedf23bb2534f8fa2c2fab8e48900e66d61af6f3262546c01"],"txID":"b33337e74de5ca8f6155003b588ae8a4d6580432d41a86d9086a244fb2960ab2","raw_data":{"contract":[{"parameter":{"value":{"owner_address":"415a523b449890854c8fc460ab602df9f31fe4293f","contract_address":"416162aff58d27a5fbd15b2f8f7ef752b2f4256086"},"type_url":"type.googleapis.com/protocol.ClearABIContract"},"type":"ClearABIContract"}],"ref_block_bytes":"0c19","ref_block_hash":"4b4f1264c3f9d924","expiration":1558685682000,"timestamp":1558685622423},"raw_data_hex":"0a020c1922084b4f1264c3f9d92440d092a0c7ae2d5a630830125f0a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e436c656172414249436f6e7472616374122e0a15415a523b449890854c8fc460ab602df9f31fe4293f1215416162aff58d27a5fbd15b2f8f7ef752b2f42560867097c19cc7ae2d"}`
Step 3. Call api: wallet/broadcasttransaction to broadcast the transaction
`curl -X POST  http://127.0.0.1:8090/wallet/broadcasttransaction -d '{"signature":["0e7e750226f01096f2f4aa0c2d03ad17d7ff57277ac3b655ecd692e3d9bd9bb822426dc779f046d79eedf23bb2534f8fa2c2fab8e48900e66d61af6f3262546c01"],"txID":"b33337e74de5ca8f6155003b588ae8a4d6580432d41a86d9086a244fb2960ab2","raw_data":{"contract":[{"parameter":{"value":{"owner_address":"415a523b449890854c8fc460ab602df9f31fe4293f","contract_address":"416162aff58d27a5fbd15b2f8f7ef752b2f4256086"},"type_url":"type.googleapis.com/protocol.ClearABIContract"},"type":"ClearABIContract"}],"ref_block_bytes":"0c19","ref_block_hash":"4b4f1264c3f9d924","expiration":1558685682000,"timestamp":1558685622423},"raw_data_hex":"0a020c1922084b4f1264c3f9d92440d092a0c7ae2d5a630830125f0a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e436c656172414249436f6e7472616374122e0a15415a523b449890854c8fc460ab602df9f31fe4293f1215416162aff58d27a5fbd15b2f8f7ef752b2f42560867097c19cc7ae2d"}'`
Return:
`{"result": true}`
The `clearContractABI` can clear the ABI of contract at the address if the account is the owner of the contract.

In case the account is not the owner of contract will throw an exception.

## Backwards Compatibility

`triggerContract` a function will push transactions on Blockchain after clear the ABI of contract.
See TriggerConstantContract for a more detailed discussion.

## Test Cases

1. The `clearContractABI` caller is the owner of contract will clear the ABI of contract at the address.
2. The `clearContractAB`I caller is not the owner of contract will throw an exception.
3. The `clearContractABI` of non-existent address will throw an exception.

