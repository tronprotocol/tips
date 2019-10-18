```
tip: xx
title: Pirvate key protection by passphrase in keystore
author: xxx<xxx@tron.network>
discussions-to: https://github.com/tronprotocol/TIPs/issues/xx
status: draft
type: Standards Track
category: TRC
created: 2019-10-17
```

## Simple Summary

This tip describes the keystore generation to store the private key in wallet. 

## Motivation

Private key is fatal important for users, which should be kept secret. Mnemonic code specified in [BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) is used to 
generate the private key, but it is not convenient for users to remember. Usually, encrypted private key is stored in keystore file and can be restored by users by passphrase. 
The proposal presents the explicit method to generate the keystore file and improve the security of users' private keys.


## Specification

### Key Derivation Function 

First, the user needs to provide the passphrase as the input of [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2). The key derivation function has five input parameters:


    K = PBKDF2(PRF, Passphrase, Salt, c, dkLen)

where
* *PRF* is a pseudorandom function, such as sha256
* *Passphrase* is the master password from which a derived key is generated
* *Salt* is a sequence of bits, known as a cryptographic salt
* *c* is the number of iterations desired
* *dkLen* is the desired bit-length of the derived key
* *DK* is the generated derived key

### Symmetric Encryption
The derived key *DK* is used as key of [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) to encrypt the real private key of user.

    C = AES-128(DK, PrivK, CTR)

where
* *DK* is the derived key
* *PrivK* is the private key of user 
* *CTR* is the counter encryption mode 
* *C* is the generated cipher text

### Message Authentication Code

MAC (Message authentication code) is used to check the correctness of derived key *DK* when the user try to decrypt the private key 
with the passphrase. [SHA3](https://en.wikipedia.org/wiki/SHA-3) is used to produce the MAC:

    mac = SHA3-256 (DK, C)

where
* *DK* is the derived key
* *C* is the cipher text of private key 
* *mac* is the generated MAC

## Rationale

The SHA256 and AES used in the proposal are all international cryptography standard, which are sufficient to ensure the security of the private key.


## Reference
https://medium.com/@julien.maffre/what-is-an-ethereum-keystore-file-86c8c5917b97