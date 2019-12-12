```
tip: 106
title: Vector Commitment In TIBC
author: @olivier
type: Tron Inter-blockchain Communication Protocol
discussions to: https://github.com/tronprotocol/TIPs/issues/106
category: TRC
status: Draft
created: 2019-12-05
```

## Summary
This document introduces the major use cases of Vector Commitment in TICP（Tron Inter-blockchain Communication Protocol） and lists all possible functions and properties in the commitment scheme that may need to be included in TICP.


## Abstract
The commitment scheme refers to a cryptographic scheme under which one can transmit encrypted messages to another, and then reveal the sent messages through a certain approach. The commitment scheme needs to ensure immutability after the transmitter has sent the encrypted message. A typical commitment includes two phases: the commit phase and the reveal phase.

A Vector Commitment (VC) is a position-binding commitment which can be opened at any position to a unique value with a succinct membership and/or non-membership proof for any elements in the vector. Merkle tree structure is a VC solution that can be opened at a logarithmic size. 

## Motivation
In the actual process of cross-chain state transition, we need to transfer an existing state from one chain to another and have the state verified on the new chain at the same time. TICP requires an efficient VC solution to prove whether or not a particular state exists in a particular path.

This protocol plans to implement the VC protocol framework first with the Merkle-tree structure and later with the VC framework based on RSA so as to meet demands for more complex opens.

## Rationale
A Merkle Proof completes membership proof through log-size proofs. In order to prove whether Value or Hash exists in a Merkle tree, the information below is needed:

1. Merkle Root
2. Hash Value that needs to be verified
3. All Hash Values from Root Node to Leaf Node along Merkle Path
4. Hash Values at the other side of nodes in Merkle Path

In normal circumstances, No.3 is optional, as all Hash Values of nodes on Merkle Path including Root Node can be calculated based on No.2 and No.4. If the calculation proves to be correct, then there truly exists a path going from Leaf Node to Root Node, which confirms the real presence of Leaf Node in the entire Merkle tree, thus completing membership proof.

## Specification

#### Datatypes

A VC scheme should comprise the following data type and be serialized. java-tron adopts Protobuf to serialize data.

##### Commitment Root

Commitment Root, constant in size, is the commitment state of the VC framework

```typescript
public class CommitmentRoot
```

##### Commitment Path

Commitment Path is a supplementary path used to verify commitment proof, and the path can be defined in any data structure.

```typescript
public class CommitmentPath
```

##### Commitment Proof

Commitment Proof indicates the membership or non-membership state of one or a group of elements and is usually combined with a known commitment root to perform verification. The proof should be succinct.

```typescript
public class CommitmentProof
```

#### Required functions

The commitment framework must support the following functions

##### Initalisation

With the getRoot function, a constant-size commitment, which can be used to verify Proofs, is generated from a set of ordinal values.

```typescript
public CommitmentRoot getRoot(List<Value> values)
```

#### Adding & Removing

We need to first define a commitment state sum that has all Commitment Paths to make the function more succinct.

```typescript
public class CommitmentTree

public CommitmentTree getTree(List<CommitmentPath> paths)
```

With add function, an element is added to a particular path of VC.

```typescript
public CommitmentRoot add(CommitmentTree tree, Path path, Value value)
```

With remove function, an element is removed from a particular path of VC.

```typescript
public CommitmentRoot remove(CommitmentTree tree, Path path)
```

#### Proof generation

createProof function produces a proof, which verifies that a particular value is included in a particular commitment.

```typescript
public CommitmentProof createProof(CommitmentRoot root, CommitmentPath path, Value value)
```

#### Proof verification

verifyProof function verifies whether a particular value verified in the particular commitment proof is correct.


```typescript
public boolean verifyProof(CommitmentRoot root, CommitmentProof proof, Value value)
```

## Implementation
coming soon

## Reference
-  [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)
-   [Vector Commitments and their Applications](https://eprint.iacr.org/2011/495.pdf)
