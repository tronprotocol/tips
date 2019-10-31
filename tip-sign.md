```
tip: xx
title: Tron Data Hashing and Signing 
author: federico<federico.zhen@tron.network>
discussions-to: https://github.com/tronprotocol/tips/issues/101
status: draft
type: Standards Track
category: TRC
created: 2019-10-31
```

## Simple Summary

Private key is not only used to sign the transaction, but also some ordinary message in practical applications. It is necessary
to distinguish the two kinds of data when signing because risks may exist if an attacker tricks users to sign semantically meaningless
which can de decoded as a valid transaction. This TIP aims to provide explicit data methods to distinguish between transaction
and ordinary message when signing. 

## Abstract

This is a standard for hashing and signing of data to distinguish the transaction and ordinary message. It also includes the typed structured data as opposed to just bytestrings based on 
[EIP712](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-712.md). It includes

*   theoretical framework for correctness of encoding functions,
*   specification of structured data,
*   safe hashing algorithm for instances of those structures,
*   safe inclusion of those instances in the set of signable messages,
*   an extensible mechanism for domain separation.

## Motivation
To prevent the potential risk when user is tricked to sign forged messages, it's necessary to provide the standard method to distinguish between transaction and ordinary message when signing. 
Since signed messages are an opaque hex string displayed to the user with little context about the items that make up the message. Furthermore, we present a scheme to encode data along with its structure Base on [EIP712](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-712.md) which allows it to be displayed to the user for verification when signing. 

## Specification

A signature scheme consists of hashing algorithm and a signing algorithm. The signing algorithm of choice is `secp256k1`. The hashing algorithm of choice is `keccak256`, this is a function from bytestrings, 𝔹⁸ⁿ, to 256-bit strings, 𝔹²⁵⁶.

### Transactions and bytestrings

There are two kinds of messages, transactions `𝕋` and bytestrings `𝔹⁸ⁿ`. These are signed using `signTransaction` and `signString` respectively. Originally the encoding function `encode : 𝕋 ∪ 𝔹⁸ⁿ → 𝔹⁸ⁿ` was defined as follows:

*   `encode(t : 𝕋) = Protobuf(t)`
*   `encode(b : 𝔹⁸ⁿ) = b`

Note: [Protobuf](https://developers.google.com/protocol-buffers) is a mechanism for serializing structured data. 

While individually they satisfy the required properties, together they do not. If we take `b = Protobuf(t)` we have a collision. To avoid the problem,  we can modify the second encoding function:

*   `encode(b : 𝔹⁸ⁿ) = "\x19TRON Signed Message:\n" ‖ len(b) ‖ b` where `len(b)` is the ascii-decimal encoding of the number of bytes in `b`.

This solves the collision between the legs since `Protobuf(t : 𝕋)` in our implementation never starts with `\x19`. Actually, the first byte should be `\x15`, which denotes the byte length of "TRON Signed Message:\n". Since developer has already altered the [source code](https://github.com/TRON-US/tronweb/commit/8ee618cba2414fb6d0fe3a214fb25fae21172922), we will leave it as it is.

### Arbitrary messages

The `eth_sign` call assumes messages to be bytestrings. In practice we are not hashing bytestrings but the collection of all semantically different messages of all different DApps `𝕄`. Unfortunately, this set is impossible to formalize. Instead we approximate it with the set of typed named structures `𝕊`. This standard formalizes the set `𝕊` and provides a deterministic injective encoding function for it.

Just encoding structs is not enough. It is likely that two different DApps use identical structs. When this happens, a signed message intended for one DApp would also be valid for the other. The signatures are compatible. This can be intended behaviour, in which case everything is fine as long as the DApps took replay attacks into consideration. If it is not intended, there is a security problem.

The way to solve this is by introducing a domain separator, a 256-bit number. This is a value unique to each domain that is 'mixed in' the signature. It makes signatures from different domains incompatible. The domain separator is designed to include bits of DApp unique information such as the name of the DApp, the intended validator contract address, the expected DApp domain name, etc. The user and user-agent can use this information to mitigate phishing attacks, where a malicious DApp tries to trick the user into signing a message for another DApp.

### Note on replay attacks

This standard is only about signing messages and verifying signatures. In many practical applications, signed messages are used to authorize an action, for example an exchange of tokens. It is _very important_ that implementers make sure the application behaves correctly when it sees the same signed message twice. For example, the repeated message should be rejected or the authorized action should be idempotent. How this is implemented is specific to the application and out of scope for this standard.

## Specification

<!-- The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (cpp-ethereum, go-ethereum, parity, ethereumj, ethereumjs, ...). -->

The set of signable messages is extended from transactions and bytestrings `𝕋 ∪ 𝔹⁸ⁿ` to also include structured data `𝕊`. The new set of signable messages is thus `𝕋 ∪ 𝔹⁸ⁿ ∪ 𝕊`. They are encoded to bytestrings suitable for hashing and signing as follows:

*   `encode(transaction : 𝕋) = RLP_encode(transaction)`
*   `encode(message : 𝔹⁸ⁿ) = "\x19Ethereum Signed Message:\n" ‖ len(message) ‖ message` where `len(message)` is the _non-zero-padded_ ascii-decimal encoding of the number of bytes in `message`.
*   `encode(domainSeparator : 𝔹²⁵⁶, message : 𝕊) = "\x19\x01" ‖ domainSeparator ‖ hashStruct(message)` where `domainSeparator` and `hashStruct(message)` are defined below.

This encoding is deterministic because the individual components are. The encoding is injective because the three cases always differ in first byte. (`RLP_encode(transaction)` does not start with `\x19`.)

The encoding is compliant with [EIP-191][eip191]. The 'version byte' is fixed to `0x01`, the 'version specific data' is the 32-byte domain separator `domainSeparator` and the 'data to sign' is the 32-byte `hashStruct(message)`.

[eip191]: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-191.md

### Definition of typed structured data `𝕊`

To define the set of all structured data, we start with defining acceptable types. Like ABIv2 these are closely related to Solidity types. It is illustrative to adopt Solidity notation to explain the definitions. The standard is specific to the Ethereum Virtual Machine, but aims to be agnostic to higher level languages. Example:

```Solidity
struct Mail {
    address from;
    address to;
    string contents;
}
```

**Definition**: A _struct type_ has valid identifier as name and contains zero or more member variables. Member variables have a member type and a name.

**Definition**: A _member type_ can be either an atomic type, a dynamic type or a reference type.

**Definition**: The _atomic types_ are `bytes1` to `bytes32`, `uint8` to `uint256`, `int8` to `int256`, `bool` and `address`. These correspond to their definition in Solidity. Note that there are no aliases `uint` and `int`. Note that contract addresses are always plain `address`. Fixed point numbers are not supported by the standard. Future versions of this standard may add new atomic types.

**Definition**: The _dynamic types_ are `bytes` and `string`. These are like the atomic types for the purposed of type declaration, but their treatment in encoding is different.

**Definition**: The _reference types_ are arrays and structs. Arrays are either fixed size or dynamic and denoted by `Type[n]` or `Type[]` respectively. Structs are references to other structs by their name. The standard supports recursive struct types.

**Definition**: The set of structured typed data `𝕊` contains all the instances of all the struct types.

### Definition of `hashStruct`

The `hashStruct` function is defined as

*   `hashStruct(s : 𝕊) = keccak256(typeHash ‖ encodeData(s))` where `typeHash = keccak256(encodeType(typeOf(s)))`

**Note**: The `typeHash` is a constant for a given struct type and does not need to be runtime computed.

### Definition of `encodeType`

The type of a struct is encoded as `name ‖ "(" ‖ member₁ ‖ "," ‖ member₂ ‖ "," ‖ … ‖ memberₙ ")"` where each member is written as `type ‖ " " ‖ name`. For example, the above `Mail` struct is encoded as `Mail(address from,address to,string contents)`.

If the struct type references other struct types (and these in turn reference even more struct types), then the set of referenced struct types is collected, sorted by name and appended to the encoding. An example encoding is `Transaction(Person from,Person to,Asset tx)Asset(address token,uint256 amount)Person(address wallet,string name)`.

### Definition of `encodeData`

The encoding of a struct instance is `enc(value₁) ‖ enc(value₂) ‖ … ‖ enc(valueₙ)`, i.e. the concatenation of the encoded member values in the order that they appear in the type. Each encoded member value is exactly 32-byte long.

The atomic values are encoded as follows: Boolean `false` and `true` are encoded as `uint256` values `0` and `1` respectively. Addresses are encoded as `uint160`. Integer values are sign-extended to 256-bit and encoded in big endian order. `bytes1` to `bytes31` are arrays with a beginning (index `0`) and an end (index `length - 1`), they are zero-padded at the end to `bytes32` and encoded in beginning to end order. This corresponds to their encoding in ABI v1 and v2.

The dynamic values `bytes` and `string` are encoded as a `keccak256` hash of their contents.

The array values are encoded as the `keccak256` hash of the concatenated `encodeData` of their contents (i.e. the encoding of `SomeType[5]` is identical to that of a struct containing five members of type `SomeType`).

The struct values are encoded recursively as `hashStruct(value)`. This is undefined for cyclical data.

### Definition of `domainSeparator`


```Solidity
domainSeparator = hashStruct(eip712Domain)
```

where the type of `eip712Domain` is a struct named `EIP712Domain` with one or more of the below fields. Protocol designers only need to include the fields that make sense for their signing domain. Unused fields are left out of the struct type.

*   `string name` the user readable name of signing domain, i.e. the name of the DApp or the protocol.
*   `string version` the current major version of the signing domain. Signatures from different versions are not compatible.
*   `uint256 chainId` the [EIP-155][eip155] chain id. The user-agent *should* refuse signing if it does not match the currently active chain.
*   `address verifyingContract` the address of the contract that will verify the signature. The user-agent *may* do contract specific phishing prevention.
*   `bytes32 salt` an disambiguating salt for the protocol. This can be used as a domain separator of last resort.

[eip155]: https://eips.ethereum.org/EIPS/eip-155

Future extensions to this standard can add new fields with new user-agent behaviour constraints. User-agents are free to use the provided information to inform/warn users or refuse signing.

## Rationale


## Test Cases 

None

## Implementation

None
