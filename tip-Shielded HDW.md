
```
tip: xx
title: Shielded Hierarchical Deterministic Wallets
author: xxx<xxx@tron.network>
discussions-to: https://github.com/tronprotocol/TIPs/issues/xx
status: draft
type: Standards Track
category: TRC
created: 2019-10-17
```


## Simple Summary

This proposal defines a mechanism for extending hierarchical deterministic wallets, as decribed in [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki),
 to support Tron's shielded addresses.

The specification has two parts. The first part defines a system for deriving a tree of key
components from a single seed. The second part shows how to use these trees in the
context of existing [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) wallets.

This specification follows the standard proposed by Zcash team [ZIP32](https://github.com/zcash/zips/blob/master/zip-0032.rst), which complements the existing use by some Tron wallets of BIP 32 and BIP 44 for transparent
Tron addresses.


## Motivation

[BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) is the standard mechanism by which wallets for Bitcoin and its derivatives  generate keys and addresses deterministically. This has several
advantages over random generation:

- Wallets only need to store a single seed (particularly useful for hardware wallets).
- A one-time backup of the seed (usually stored as a word phrase [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)) can be used to recover funds
  from all future addresses.
- Keys are arranged into a tree of chains, enabling wallets to represent "accounts" or other high-level
  structures.
- View authority or spend authority can be delegated independently for sub-trees without compromising the
  master seed.

At present, Tron network has updated to support the shielded addresses, so it is necessary to provide the standard mechanism for shielded hierarchical deterministic wallets.  

## Conventions

Most of the notation and functions used in this TIP are defined here for convenience:

- truncate<sub>k</sub>(*S*) means the sequence formed from the first *k* elements of *S*.

- *a* || *b* means the concatenation of sequences *a* then *b*.

- [*k*] *P* means scalar multiplication of the elliptic curve point *P* by the scalar *k*.

- LEOS2IP<sub>l</sub> (*S*) is the integer in range {0..2<sup>l</sup> -1} represented in little-endian order
  by the byte sequence *S* of length *l*/8.

- I2LEBSP<sub>l</sub> (*k*) is the sequence of *l* bits representing *k* in little-endian order.

- LEBS2OSP<sub>l</sub> (*B*) is defined as follows when *l* is a multiple of 8: convert each group of 8 bits
  in *B* to a byte value with the least significant bit first, and concatenate the resulting bytes in the
  same order as the groups.

- repr<sub>J</sub> (*P*) is the representation of the Jubjub elliptic curve point *P* as a bit sequence.

- BLAKE2b-256(*p*, *x*) refers to unkeyed BLAKE2b-256 in sequential mode, with an output digest length of
  32 bytes, 16-byte personalization string *p*, and input *x*.

- BLAKE2b-512(*p*, *x*) refers to unkeyed BLAKE2b-512 in sequential mode, with an output digest length of
  64 bytes, 16-byte personalization string *p*, and input *x*.

- PRF<sup>expand</sup> (*sk*, *t*) := BLAKE2b-512("Tron_ExpandSeed", *sk* || *t* )

- ToScalar(*x*) := LEOS2IP<sub>512</sub> (*x*) (mod *r*<sub>J</sub> ), where *r*<sub>J</sub> is the order
  of the Jubjub large prime subgroup.

- DiversifyHash(*d*) maps a diversifier *d* to a base point on the Jubjub elliptic curve, or to ⊥ if the
  diversifier is invalid. 

The following [FPE](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-38G.pdf) algorithm standardized is used:

- FF1-AES256.Encrypt(*key*, *tweak*, *x*) refers to the FF1 encryption algorithm using AES with a
  256-bit *key*, and parameters *radix* = 2, *minlen* = 88, *maxlen* = 88. It will be used only with
  the empty string "" as the *tweak*. *x* is a sequence of 88 bits, as is the output.

We also define the following conversion function:

- I2LEOSP<sub>l</sub> (*k*) is the byte sequence *S* of length *l*/8 representing in little-endian order the
  integer *k* in range {0..2<sup>l</sup> -1}. It is the reverse operation of LEOS2IP<sub>l</sub> (*S*).

Implementors should note that this ZIP is consistently little-endian (in keeping with the Sapling
specification), which is the opposite of BIP 32.

We adapt the path notation of [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) to describe shielded HD paths, using apostrophes to
indicate hardened derivation (i' = i + 2<sup>31</sup>\ ) as in [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki):

- CDKsk(CDKsk(CDKsk(m, a'), b), c) is written as m / a' / b / c
- CDKfvk(CDKfvk(CDKfvk(M, a), b), c) is written as M / a / b / c


## Specification: Key Derivation

### Extended Keys


BIP 32 defines a method to derive a number of child keys from a parent key. In order to prevent these from
depending solely on the parent key itself, both the private and public keys are extended with a 32-byte chain
code. We similarly extend Sapling keys with a chain code here. However, the concepts of "private" and "public"
keys in BIP 32 do not map cleanly to shielded key components. We take the following approach:

- We derive child expanded spending keys, rather than spending keys. This enables us to
  implement both hardened and non-hardened derivation modes.

- We do not derive public keys directly, as this would prevent the use of diversified addresses.
  Instead, we derive full viewing keys, from which payment addresses can be generated. This maintains
  the trust semantics of BIP 32: someone with access to a BIP 32 extended public key is able to view all
  transactions involving that address, which a full viewing key also enables.

We represent a extended spending key as (*ask*, *nsk*, *ovk*, *dk*, *c*), where (*ask*, *nsk*, *ovk*)
is the normal expanded spending key, *dk* is a diversifier key, and *c* is the chain code.

We represent a extended full viewing key as (*ak*, *nk*, *ovk*, *dk*, *c*), where (*ak*, *nk*, *ovk*)
is the normal Sapling full viewing key, *dk* is the same diversifier key as above, and *c* is the chain code.

### The helper functions

Define EncodeExtSKParts(*ask*, *nsk*, *ovk*, *dk*) := I2LEOSP<sub>256</sub> (*ask*) || I2LEOSP<sub>256</sub> (*nsk*) || *ovk* || *dk*.

Define EncodeExtFVKParts(*ak*, *nk*, *ovk*, *dk*) := LEBS2OSP<sub>256</sub> (repr<sub>J</sub> (*ak*)) || LEBS2OSP<sub>256</sub> (repr<sub>J</sub> (*nk*)) || *ovk* || *dk*.

### Master Key Generation

Let *S* be a seed byte sequence of a chosen length, which MUST be at least 32 bytes.

- Calculate *I* = BLAKE2b-512("TronIPXX", *S*).
- Split *I* into two 32-byte sequences, *I*<sub>L</sub> and *I*<sub>R</sub> .
- Use *I*<sub>L</sub> as the master spending key *sk*<sub>m</sub> , and *I*<sub>R</sub> as the master chain code
  *c*<sub>m</sub>.
- Calculate *ask*<sub>m</sub> , *nsk*<sub>m</sub> , and *ovk*<sub>m</sub> via the standard derivation function:

  - *ask*<sub>m</sub> = ToScalar(PRF<sup>expand</sup> (*sk*<sub>m</sub> , [0x00]))
  - *nsk*<sub>m</sub> = ToScalar(PRF<sup>expand</sup> (*sk*<sub>m</sub> , [0x01]))
  - *ovk*<sub>m</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*sk*<sub>m</sub> , [0x02]))

- Calculate *dk*<sub>m</sub> similarly:

  - *dk*<sub>m</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*sk*<sub>m</sub> , [0x10]))

- Return (*ask*<sub>m</sub> , *nsk*<sub>m</sub> , *ovk*<sub>m</sub> , *dk*<sub>m</sub> , *c*<sub>m</sub> ) as the
  master extended spending key *m*.

### Child Key Derivation

As in BIP 32, the method for deriving a child extended key, given a parent extended key and an index *i*,
depends on the type of key being derived, and whether this is a hardened or non-hardened derivation.

#### Deriving a child extended spending key

CDKsk((*ask*<sub>par</sub> , *nsk*<sub>par</sub> , *ovk*<sub>par</sub> , *dk*<sub>par</sub> , *c*<sub>par</sub> ), *i*) →
(*ask*<sub>i</sub> , *nsk*<sub>i</sub> , *ovk*<sub>i</sub> , *dk*<sub>i</sub> , *c*<sub>i</sub> )

- Check whether *i* ≥ 2<sup>31</sup> (whether the child is a hardened key).

  - If so (hardened child): let *I* = PRF<sup>expand</sup> (*c*<sub>par</sub> , [0x11] || EncodeExtSKParts(*ask*<sub>par</sub> , *nsk*<sub>par</sub> , *ovk*<sub>par</sub> , *dk*<sub>par</sub> ) || I2LEOSP<sub>32</sub> (*i*))
  - If not (normal child):  let *I* = PRF<sup>expand</sup> (*c*<sub>par</sub> , [0x12] || EncodeExtFVKParts(*ak*<sub>par</sub> , *nk*<sub>par</sub> , *ovk*<sub>par</sub> , *dk*<sub>par</sub> ) || I2LEOSP<sub>32</sub> (*i*))
    where (*nk*<sub>par</sub> , *ak*<sub>par</sub> , *ovk*<sub>par</sub> ) is the full viewing key derived from
    (*ask*<sub>par</sub> , *nsk*<sub>par</sub> , *ovk*<sub>par</sub> ) as described in [#sapling-key-components]_.

- Split *I* into two 32-byte sequences, *I*<sub>L</sub> and *I*<sub>R</sub> .
- Let *I*<sub>ask</sub> = ToScalar(PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x13]))
- Let *I*<sub>nsk</sub> = ToScalar(PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x14]))
- Return:

  - *ask*<sub>i</sub> = *I*<sub>ask</sub> + *ask*<sub>par</sub>
  - *nsk*<sub>i</sub> = *I*<sub>nsk</sub> + *nsk*<sub>par</sub>
  - *ovk*<sub>i</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x15] || *ovk*<sub>par</sub> ))
  - *dk*<sub>i</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x16] || *dk*<sub>par</sub> ))
  - *c*<sub>i</sub> = *I*<sub>R</sub>

#### Deriving a child extended full viewing key

Let *G* and *H* be the base point in elliptic curve.

CDKfvk((*ak*<sub>par</sub> , *nk*<sub>par</sub> , *ovk*<sub>par</sub> , *dk*<sub>par</sub> , *c*<sub>par</sub> ), *i*) →
(*ak*<sub>i</sub> , *nk*<sub>i</sub> , *ovk*<sub>i</sub> , *dk*<sub>i</sub> , *c*<sub>i</sub> )

- Check whether *i* ≥ 2<sup>31</sup> (whether the child is a hardened key).

  - If so (hardened child): return failure
  - If not (normal child):  let *I* = PRF<sup>expand</sup> (*c*<sub>par</sub> , [0x12] || EncodeExtFVKParts(*ak*<sub>par</sub> , *nk*<sub>par</sub> , *ovk*<sub>par</sub> , *dk*<sub>par</sub> ) || I2LEOSP<sub>32</sub> (*i*))

- Split *I* into two 32-byte sequences, *I*<sub>L</sub> and *I*<sub>R</sub> .
- Let *I*<sub>ask</sub> = ToScalar(PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x13]))
- Let *I*<sub>nsk</sub> = ToScalar(PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x14]))
- Return:

  - *ak*<sub>i</sub> = [*I*<sub>ask</sub>] G + *ak*<sub>par</sub>
  - *nk*<sub>i</sub> = [*I*<sub>nsk</sub>] H + *nk*<sub>par</sub>
  - *ovk*<sub>i</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x15] || *ovk*<sub>par</sub> ))
  - *dk*<sub>i</sub> = truncate<sub>32</sub> (PRF<sup>expand</sup> (*I*<sub>L</sub> , [0x16] || *dk*<sub>par</sub> ))
  - *c*<sub>i</sub> = *I*<sub>R</sub>

### Diversifier derivation


The 88-bit diversifiers for a extended key are derived from its diversifier key *dk*. To prevent the
diversifier leaking how many diversified addresses have already been generated for an account, we make the
sequence of diversifiers pseudorandom and uncorrelated to that of any other account. In order to reach the
maximum possible diversifier range without running into repetitions due to the birthday bound, we use
FF1-AES256 as a Pseudo-Random Permutation as follows:

- Let *j* be the index of the desired diversifier, in the range 0 .. 2<sup>88</sup> -1.
- *d*<sub>j</sub> = FF1-AES256.Encrypt(*dk*, "", I2LEBSP<sub>88</sub> (*j*)).

A valid diversifier *d*<sub>j</sub> is one for which DiversifyHash(*d*<sub>j</sub>) ≠ ⊥.
For a given *dk*, approximately half of the possible values of *j* yield valid diversifiers.

The default diversifier for a Sapling extended key is defined to be *d*<sub>j</sub>\ , where *j* is the
least nonnegative integer yielding a valid diversifier.


## Specification: Wallet usage


Existing HD wallets all use [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) to organize their derived keys. In order to
more easily mesh with existing user experiences, we broadly follow BIP 44's design here. However, we have
altered the design where it makes sense to leverage features of shielded addresses.

### Key path levels

We have the following three path levels at the top, all of which use hardened
derivation:

- ``purpose``: a constant set to 32' (or 0x80000020)  following the BIP 43 recommendation. It indicates that
  the subtree of this node is used according to this specification.

- ``coin_type``: a constant identifying the cybercoin that this subtree's keys are used with. For
  compatibility with existing BIP 44 implementations, we use the same constants as defined in [SLIP44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)
  . Note that in keeping with that document, all cybercoin testnets share ``coin_type`` index 1.

- ``account``: numbered from index 0 in sequentially increasing manner. Defined as in [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki).

Follow the [ZIP32](https://github.com/zcash/zips/blob/master/zip-0032.rst), we don not have a `change` path level. The use of change addresses in Bitcoin
is to increase the difficulty of tracking users on the transaction graph, by segregating
external and internal address usage. Shielded addresses are never publicly visible in transactions, which
means that sending change back to the originating address is indistinguishable from using a change address.

### Key Path

Sapling provides a mechanism to allow the efficient creation of diversified payment addresses with the same
spending authority. A group of such addresses shares the same full viewing key and incoming viewing key, and
so creating as many unlinkable addresses as needed does not increase the cost of scanning the block chain for
relevant transactions.

The above key path levels include an account identifier, which in all user interfaces is represented as a
"bucket of funds" under the control of a single spending authority. Therefore, wallets implementing Sapling
ZIP 32 derivation MUST support the following path for any account in range {0..2<sup>31</sup> -1}:

    m / purpose' / coin_type' / account'

Furthermore, wallets MUST support generating the default payment address (corresponding to the default
diversifier as defined above) for any account they support. They MAY also support generating a stream of
payment addresses for a given account, if they wish to maintain the user experience of giving a unique
address to each recipient.

Note that a given account can have a maximum of approximately 2<sup>87</sup> payment addresses, because each
diversifier has around a 50% chance of being invalid.

If in certain circumstances a wallet needs to derive independent spend authorities within a single account,
they MAY additionally support a non-hardened ``address_index`` path level as in [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki):

    m / purpose' / coin_type' / account' / address_index


## Specification: Fingerprints and Tags


### Full Viewing Key Fingerprints and Tags


A full viewing key with raw encoding *FVK*  is given by:

    BLAKE2b-256("TronFVFP", FVK)

It MAY be used to uniquely identify a particular Sapling full viewing key.

A "full viewing key tag" is the first 4 bytes of the corresponding full viewing key
fingerprint. It is intended for optimizing performance of key lookups, and MUST NOT be assumed to
uniquely identify a particular key.



### Seed Fingerprints

A "seed fingerprint" for the master seed *S* of a hierarchical deterministic wallet is given by:

    BLAKE2b-256("Tron_HD_Seed_FP", S)

It MAY be used to uniquely identify a particular hierarchical deterministic wallet.

No corresponding short tag is defined.


## Specification: Key Encodings

The following encodings are analogous to the ``xprv`` and ``xpub`` encodings defined
in BIP 32 for transparent keys and addresses. Each key type has a raw representation
and a [Bech32](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki) encoding.


### Extended Spending Keys

A Sapling extended spending key (*ask*, *nsk*, *ovk*, *dk*, *c*), at depth *depth*,
with parent full viewing key tag *parent_fvk_tag* and child number *i*, is
represented as a byte sequence:

  I2LEOSP<sub>8</sub> (*depth*) || *parent_fvk_tag* || I2LEOSP<sub>32</sub> (*i*) || *c* || EncodeExtSKParts(*ask*, *nsk*, *ovk*, *dk*)

For the master extended spending key, *depth* is 0, *parent_fvk_tag* is 4 zero bytes,
and *i* is 0.

When encoded as Bech32, the Human-Readable Part is ``secret-extended-key-main``
for the production network, or ``secret-extended-key-test`` for the test network.

Extended full viewing keys
----------------------------------

A extended full viewing key (*ak*, *nk*, *ovk*, *dk*, *c*), at depth *depth*,
with parent full viewing key tag *parent_fvk_tag* and child number *i*, is
represented as a byte sequence:

   I2LEOSP<sub>8</sub> (*depth*) || *parent_fvk_tag* || I2LEOSP<sub>32</sub> (*i*) || *c* || EncodeExtFVKParts(*ak*, *nk*, *ovk*, *dk*)

For the master extended full viewing key, *depth* is 0, *parent_fvk_tag* is 4 zero bytes,
and *i* is 0.

When encoded as Bech32, the Human-Readable Part is ``zxviews`` for the production
network, or ``zxviewtestsapling`` for the test network.


## Rationale

We follow the standard proposed by Zcash team [ZIP32](https://github.com/zcash/zips/blob/master/zip-0032.rst) and provide a mechanism for shielded hierarchical deterministic wallets.


## Test Cases

TBC

## Implementation

* https://github.com/zcash-hackworks/zip32
* https://github.com/zcash/librustzcash/pull/29
* https://github.com/zcash/zcash/pull/3447
* https://github.com/zcash/zcash/pull/3492


## References

https://github.com/zcash/zips/blob/master/zip-0032.rst