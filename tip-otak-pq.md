---
tip: XXXX
title: One-Time Active Keys for Post-Quantum Security (OTAK-PQ)
author: Ali (@alichatme)
status: Draft
type: Standards Track
category: Core
created: 2026-06-07
discussions-to: https://github.com/tronprotocol/tips/issues/890
---
# Summary

This TIP adds the capability of One-Time Access Keys (or "child keys" for short) to the Tron network.

## One-Time Access Key (or "Child Key"):

(One-Time Access Key):
A key that is derived from one of the account’s Access Keys according to the TRC-102 standard, and whose membership in the account’s authorized key set is proven via a Merkle Proof and the Merkle Root recorded in the network’s State. Each one-time access key, after its first successful use, is permanently considered consumed and can no longer be used to create a valid transaction. The signature of the transaction associated with this key is published on the blockchain and becomes part of the transaction history only after its inactive status has been recorded in the network.

. Based on this architectural model, with the addition of the child key to the blockchain network, each account is only permitted to send transactions by signing using a child key.
. If a transaction is signed and sent with a key that is not a valid child key whose membership can be proven via a Merkle Proof, network nodes must reject the transaction without recording the signature and return the OTAK-PQ error in the validation response.
. Based on this error code, wallets can display an appropriate guidance message to the user; for example:
“This transaction is not compatible with OTAK-PQ security requirements. Please use a wallet version that supports child keys.”

. After sending a transaction with a child key to the network and its confirmation by nodes, the status of the child key changes to Consumed. After this status is recorded in the network State, the transaction and its corresponding signature are published on the blockchain and in blockchain explorers according to network protocols.

. This feature significantly reduces Tron’s exposure to threats based on key recovery from the history of recorded signatures on the network.
Because even if an attacker breaks the signature of a child key transaction, they will not gain access to the account’s assets controlled by the Access keys.
___
___
# Security features of an account before its first outgoing transaction

When a new account is created on the Tron network, until the first on-chain signature is published, its exposure to certain threat scenarios based on quantum computing is significantly reduced, subject to the following factors:

### 1. Condition of non-disclosure of public key in signature form:

. As long as an account’s or wallet’s transaction history contains only deposit operations and no outgoing transaction has been made from it.
In the absence of recorded signatures on the blockchain, no data is available to execute public-key recovery algorithms.
Therefore, the exposure to attacks based on signature analysis is significantly reduced at this stage.
. In this state, only the hash of the public key, i.e., the address, is visible and available for the account.

. Hence, it can be concluded that such wallets in the short term, i.e., before sending the first transaction to the network, will have much lower exposure to certain threats based on signature analysis.

### 2. Critical moment: the account’s first transaction

. As soon as any outgoing transaction is made (even a partial transfer of assets), the public key is automatically recorded on the blockchain in the form of a signature.
. If quantum computers with sufficient operational capability and the ability to effectively execute Shor’s algorithm at the required scale become a reality, recovering the private key from the public key will become theoretically possible.

. Obviously, this threat extends to all remaining assets in the account.

. This proposal introduces a new security model for Tron network accounts in which Access keys do not participate in the signing process of on-chain transactions and their signatures are not published on the network.
For each transaction, the wallet derives a child key from the Access Keys, generates the corresponding Merkle Proof, and signs the transaction with that child key and sends it to the network.

## Each child key is valid for only one transaction, and its validation is performed by nodes at the moment of transaction processing.

The validity of the child key is proven through the Merkle Proof provided in the transaction and the Merkle Root stored in the account. Nodes do not need to reconstruct the TRC-102 derivation process or validate the mathematical relationship between Access Keys and Child Keys.

The process is defined as follows:

1. Nodes check that the transaction signature has been provided by a valid child key; otherwise, the transaction is rejected.
2. Nodes check that the child key has not been used before and that its status in the network State is not in the Consumed state.
3. If the signature is valid and the Merkle Proof validation against the Merkle Root stored in the account State succeeds, the transaction enters the confirmation phase.
4. After the transaction is confirmed, the child key is marked as consumed (one-time-use). This status is recorded in the network state.
5. The transaction and its corresponding signature are recorded and viewable on the blockchain and explorers like TronScan according to standard network protocols.

## Limited scope of each security incident

Even if, in the future, an attacker is able to recover the private key of a child key using advanced cryptographic methods or new computing technologies, this incident will only affect that specific consumed child key.
Since that key has already been deactivated:
. It cannot be reused.
. It cannot sign a new transaction.
. No active operational permission is attached to it.
. The security of other child keys is not affected.
. It does not alone provide enough information for the attacker to recover the account’s Access Keys.
Consequently, the OTAK-PQ architecture limits the impact of any possible security incident to a single child key and prevents its spread to other components of the account.
___
___
# Abstract:

Shor’s algorithm in quantum computing has the ability to solve the discrete logarithm problem and thus can theoretically threaten security based on elliptic curves (ECC/ECDSA). In the current Tron architecture, transaction signatures are permanently recorded on the blockchain, which can increase the cryptographic attack surface in the long term.

## Proposed OTAK-PQ model

This proposal presents a security model based on Key Layer Separation, in which:

. Access keys never directly participate in signing operational network transactions.

. Access keys are used only for deriving child keys at the wallet level.

. Each transaction is signed with a Child Key.

. After the transaction is processed by nodes, the Child Key is marked as consumed.

. After the child key is deactivated, the transaction signature is published on the network history.

## Network mechanism

In the OTAK-PQ architecture, the wallet locally generates a set of Child Keys according to the TRC-102 standard.
. A Merkle Tree of the child keys is constructed.
. The resulting Merkle Root is recorded in the network State through a Bootstrap process.
. After successful Bootstrap completion, the account transitions from the Bootstrap Pending state to Active.

### For each transaction:
. The wallet selects a new unused Child Key.
. Generates the corresponding Merkle Proof.
. Signs the transaction with that Child Key.

### Network nodes accept the transaction only if:
. The signature is valid.
. The Child Key has not been consumed before.
. The Merkle Proof is valid.
. The Child Key belongs to the Merkle Root stored in the account.

### After transaction confirmation:
. The Child Key is recorded as consumed in the network State.
. The transaction is published on the blockchain according to standard network protocols.
. The Child Key can no longer be reused.

## Role of Access Keys in the OTAK-PQ security model

Access Keys have no direct role in signing network transactions and are used only at the wallet layer to generate child keys.
Consequently:
. No direct signatures from Access Keys are recorded in the public history of blockchain transactions.
. Each child key has its own independent key pair, but is deterministically derived from the Access Key.
. Even if a Child Key is compromised, access to the main account is not possible.

## Cryptographic separation of Access Keys and child keys

In the OTAK-PQ architecture, both Access Keys and child keys are deterministically generated from the user’s master Seed according to the TRC-102 standard.
Although all these keys are derived from a common root, from a cryptographic and operational perspective, each child key has its own independent key pair and acts as a separate cryptographic identity.

## Important feature of OTAK-PQ: operational independence of child keys

Each child key has its own independent public and private key and is used only to perform a single transaction.
After the transaction is successfully processed by network nodes, the child key is recorded as Consumed in the network State and becomes permanently operationally invalid.
___
___
# Motivation

### In the current Tron architecture:

. One active authorized key can sign thousands of transactions.
. Signatures remain on the blockchain forever.
. Breaking one signature can lead to permanent control of the main account by the attacker.
. The main account key is exposed many times over time.

### Proposed solution: using child keys (OTAK-PQ)

. Access Keys are used solely as the Root of Trust to generate child keys.
. The wallet deterministically generates a set of child keys according to the TRC-102 standard and records their Merkle Root on the network during the Bootstrap process.
. Each transaction is signed by a separate child key.
. The validity of each child key is verified through the Merkle Proof and the Merkle Root stored in the network State.
. After the first successful use, the child key is permanently marked as consumed.
. If the private key of a child key is recovered or broken from its recorded signature, the attacker will only gain access to that consumed key, and because it is deactivated after use, there is no valid way to access assets controlled by the Access Keys or other child keys.
___
___
# Brief overview of all existing solutions for facing the quantum threat

### 1. Changing the signature algorithm to Post-Quantum (e.g., ML-DSA)

. Advantages: Long-term security, provided no new breaking algorithms like Shor or more powerful computational computers are discovered.
. Disadvantages: Requires changing the entire protocol, increased signature size, high cost, increased computational cost, signature verification and node resource consumption, extra load on network nodes.

### 2. Child keys (OTAK-PQ)

Advantages:

. Almost no need to change the current network signature algorithm.
. No significant decrease in transaction throughput and processing speed.
. No significant processing overhead for nodes.
. Compatible with current Tron infrastructure.
. Usable and compatible with current and future signature algorithms.
. Easy migration to new cryptographic algorithms if needed.
. Drastic reduction in the impact of attacks based on key recovery from recorded signatures, by limiting the validity of each signature to a single-use child key.
. Usable as a complementary security layer even if the network migrates to post-quantum algorithms.

Disadvantages:
. Requires wallets to support the OTAK-PQ architecture.
. Requires adding a Bootstrap mechanism for initial account setup.
. Requires storing the Merkle Root and validating Merkle Proofs at the network protocol level.
. Requires maintaining the consumed status of child keys in the network State.
. Increased implementation complexity compared to the traditional model of direct signing with Access Keys.
___
___
# Goal of this proposal

This proposal changes the transaction signature generation and validation process on the network as follows:
Access Keys
↓
Child key derivation and Merkle Proof generation
↓
Transaction signing by child key
↓
Signature and Merkle Proof validation by nodes
↓
Transaction execution
↓
Mark child key as consumed
↓
Public broadcast of transaction and child key signature on the network

Consequently, even if an attacker in the future can analyze a transaction signature or recover the private key corresponding to a child key:
. That child key will no longer be valid, because after transaction confirmation it is recorded as consumed in the network State.
. The child key is permanently deactivated after its first use and cannot be reused to create a valid transaction.
. The relationship between the child key and the Access Keys according to the TRC-102 standard is a one-way function; therefore, recovering Access Keys from a child key is not possible.
. The data used to prove initial account ownership during the Bootstrap process is not part of the account’s operational history; only the final validation result is stored in the network State.
. Each child key, past or future, is cryptographically independent of other child keys, and compromising one child key has no impact on the security of the Access Keys or other child keys.
___
___
# Secure Bootstrap Protocol

## Necessity

. In the OTAK-PQ security model, the fundamental principle is non-publication of Access Key signatures on the blockchain. Since network nodes need a proof-of-ownership mechanism to accept the initial Merkle Root and activate the account’s security structure, the account creation process in OTAK-PQ differs from the current Tron model.
. For this purpose, this proposal adds a new stage called the Secure Bootstrap Protocol to the Tron protocol.

## Account states in OTAK-PQ

OTAK-PQ accounts can be in one of two states:
Bootstrap Pending
Active

### Stage One: Creating the account security structure
The wallet, locally and offline:
. Generates Access Keys from the Seed.
. Derives a set of child keys according to the TRC-102 standard.
. Builds a Merkle Tree of the child keys.
. Calculates the Merkle Root.
Then the wallet sends a Bootstrap Request to the network. Because the account is in the Bootstrap Pending state and has no assets to pay fees, this transaction is processed by nodes as a fee-exempt transaction. The Bootstrap Request includes:

· Account address
· Merkle Root
· OTAK-PQ security parameters
· Initial account ownership proof
  
### Stage Two: Bootstrap validation
Network nodes receive the Bootstrap Request and:
. Verify the validity of the initial ownership proof.
. Validate the structure of the submitted data.
. Reach consensus on accepting or rejecting the request.
  In this stage, validation data is used only for the verification process, and the bootstrap request signature is not published in the public network transaction history.

### Stage Three: Recording the Bootstrap result
After nodes reach consensus:
The account’s Merkle Root is recorded in the network State.
The BootstrapCompleted field is set to true.
The account status changes from Bootstrap Pending to Active.
Only the validation result is stored in the permanent network State; the temporary data used for initial ownership proof does not become part of the account’s operational history.

## Restriction for accounts in Bootstrap Pending state

In the Bootstrap Pending state, Access Keys are permitted only to submit the Bootstrap Request required to activate the account.

. Wallets SHOULD NOT expose the account address for operational use before the account has been successfully activated.

. A newly created account remains in the Bootstrap Pending state until the Bootstrap process completes successfully.

. An account in the Bootstrap Pending state MUST NOT participate in the network's economic activity.

Before Bootstrap completion:

. The Merkle Root has not yet been permanently recorded.

. The initial ownership verification has not yet been completed.

. OTAK-PQ validation rules are not yet active.

. The account MUST NOT send or receive assets.

. If a transfer is submitted to an account that is still in the Bootstrap Pending state, network nodes MUST reject the transaction because the destination account is not yet active. The transaction is treated as a failed transaction according to the normal network validation rules, and no assets are transferred.

This rule guarantees that an account cannot participate in the network economy until its OTAK-PQ security structure has been successfully established.

## Account activation

After successful Bootstrap completion:
. The account is able to receive assets.
. OTAK-PQ rules are activated for the account.
. Access Keys are no longer permitted to directly sign operational network transactions.
. All account operations will be performed through valid child keys.

## Transaction validation

For each transaction:
. The wallet generates a new child key.
. Calculates the corresponding Merkle Proof.
. Signs the transaction with that child key.

Nodes:
. Validate the signature.
. Match the Merkle Proof against the Merkle Root stored in the account.
. Check that the child key has not been consumed before.

After confirmation:
. The transaction is executed.
. The child key is marked as consumed.
. The signature published on the blockchain corresponds only to that child key and occurs after the child key has been deactivated.

## Account Recovery

In the OTAK-PQ model, all Access Keys, the Merkle Root, and child keys are deterministically generated from the user’s master Seed according to the TRC-102 standard.
Therefore, the network does not need to store private keys, child keys, or derivation paths.
In case of device or wallet loss:

. The user enters their master Seed.
. The wallet regenerates the Access Keys.
. The child key tree structure is regenerated, and the calculated Merkle Root is matched against the value stored in the network State.
. All unused child keys will be regeneratable.
. The consumed status of child keys is determined via the network State, and keys marked as Consumed cannot be reused even after account recovery.

Because the derivation process is completely deterministic, account recovery requires no additional information beyond the Seed.
Consequently, OTAK-PQ retains all HD Wallet capabilities and does not introduce a new recovery mechanism.

## Required changes to the Tron protocol

To support OTAK-PQ, the following protocol-level changes are required:

. Add Bootstrap Pending state for newly created accounts.

. Add a new Bootstrap Request message or transaction to record the initial account Merkle Root.

. Add a BootstrapCompleted field in the account state.

. Store the Merkle Root in the account State as the Root of Trust for child key validation.

. Add Merkle Proof validation mechanism in nodes.

. Add mechanism for consumption and permanent deactivation of child keys after first successful use.

. Prevent Bootstrap Pending accounts from receiving assets until Bootstrap completes successfully.

. Enforce a protocol restriction that, after Bootstrap completes, direct signing of operational account transactions by Access Keys is disallowed.

## Security outcome

In the OTAK-PQ architecture, after the Bootstrap process is complete, all signatures published on the blockchain belong to child keys.

## Consequently:

. Access Keys are not used in signing operational account transactions, and no direct signature from them is recorded in the network’s operational history.
. Each signature corresponds only to a temporary child key.
. Each child key becomes operationally invalid after use.
. Compromise of one child key has no impact on the security of the Access Keys or other child keys.
. The impact of any possible attack is limited to a single transaction.
. The account receives the full OTAK-PQ security structure before entering the network’s economic cycle.
___
___
# OTAK-PQ architecture

### 1. Fundamental principle of the architecture

OTAK-PQ is based on the principle of “non-publication of Access Key signatures.”
   In this architecture, keys with access to the account (Access Keys), including the Owner Key and Active Keys, are never directly used to sign on-chain transactions.
   Access Keys act solely as the account’s Root of Trust and provide the basis for generating the child key structure at the wallet level.
   After the Bootstrap process completes successfully, all account operations are performed exclusively through child keys.
   If a transaction signed directly by one of the Access Keys is sent, network nodes must reject the transaction and return an OTAK-PQ error.

### 2. Child key generation

 The wallet uses the TRC-102 standard (based on BIP44) to deterministically generate a set of child keys from the Access Keys.

   Conceptual example:

   Seed
   ↓
   Access Keys
   ↓
   Child Key #0
   Child Key #1
   Child Key #2
   …

Each child key:
. Has its own independent public and private key.
. Is considered cryptographically independent of other child keys.
. Is valid for only one transaction.
. Due to the one-way nature of the derivation process, recovering Access Keys from it is impossible.
. After successful transaction confirmation, the child key identifier is recorded as Consumed in the network State. Only after this status is recorded is the transaction and its corresponding signature published on the blockchain.

### 3. Merkle tree structure

. In the OTAK-PQ architecture, child keys are organized into a Merkle Tree.

The wallet locally and offline:
. Generates the child keys.
. Creates the Merkle Tree.
. Calculates the Merkle Root.

During the Bootstrap process:
. Only the Merkle Root is recorded in the account State.
. Child keys are not stored on the network.
. The network does not retain any version of child private or public keys.

The Merkle Root serves as the account’s cryptographic root of trust for validating all child keys.

### 4. Storage structure of the Merkle Root in the account

In the OTAK-PQ architecture, the network does not need to store the list of child keys. The only information stored in the account State is:

· merkle_root: the root of the child key Merkle tree.
· bootstrap_completed: the status of Bootstrap completion.

The precise implementation details of the above data structures at the protocol level require review by the Tron core development team, and if this TIP is accepted, the final design will be carried out by them.

### 5. Transaction submission process
   
For each transaction:
. The wallet selects an unused child key.
. Signs the transaction with that key.
. Calculates the Merkle Proof for that key.
. Sends the transaction, signature, and Merkle Proof to the network.

The process is as follows:

   Access Keys
   ↓
   Child key derivation
   ↓
   Merkle Proof generation
   ↓
   Transaction signing
   ↓
   Send to network

### 6. On-network validation

Network nodes, upon receiving a transaction:

   . Verify the digital signature of the transaction.
   . Validate the provided Merkle Proof.
   . Check that the Merkle Proof matches the Merkle Root stored in the account State.
   . Check that the account is in Active state and Bootstrap is completed.
   . Check that the child key has not been consumed before.
   . After successful transaction confirmation, the child key identifier is recorded as Consumed in the network State. Only after this status is recorded are the transaction and its corresponding signature published on the blockchain.
   . In this process, nodes have no need to rebuild the derivation process or check the cryptographic relationship between the Access Key and the child key.

### 7. One-time use key consumption model

Each child key can be used only once.
   
After successful transaction confirmation:
. The transaction is executed.
. The child key identifier is recorded in the network State as consumed or nullifier.
. The possibility of reusing that key is permanently eliminated.

If an attempt is made to reuse a consumed key:
. The transaction is rejected.
. An OTAK-PQ error is returned.

### 8. Child key management in the wallet

Child key generation is completely deterministic.

   Therefore:
. All child keys can be generated from a single Seed.
. The wallet can generate millions of child keys locally.
. There is no need to register keys separately on the network.
. There is no need to maintain multiple independent backups.
. Full recovery of the account structure is possible only with the master Seed.

### 9. Consumed Child Key Tracking Model

In the OTAK-PQ architecture, the network does NOT store any consumed-key set, bitmap, or list of used child keys. The OTAK-PQ-related state per account is minimal and includes only:

· merkle_root
· bootstrap_completed
· last_used_child_index

The validation model is based on mandatory sequential ordering of child keys.

For each new transaction, nodes verify:

. The transaction signature is valid.

. The Merkle Proof is valid against the Merkle Root stored in the account.

. The provided child key exactly matches the next expected index.

After successful transaction confirmation, last_used_child_index is updated accordingly.

In fact, last_used_child_index serves the same role as a nonce in the EIP-8202 model, but specifically for the child key lifecycle and without requiring transaction history scanning for account recovery.

As a result:

· No list of consumed keys is maintained.
· No bitmap or consumed-key set is required.
· No state growth occurs per transaction.
· The OTAK-PQ-related state size per account remains constant regardless of transaction count.

Therefore, no pruning or archival mechanisms are needed for consumed child keys.

This sequential index model also naturally prevents replay attacks, because any transaction referencing a previously used child key will be rejected during validation.

### 10. Rotation Window


Purpose

To ensure uninterrupted long-term account operation and eliminate the possibility of exhausting an active Merkle Tree, OTAK-PQ introduces a Rotation Window.

A Rotation Window is a reserved range of Child Keys located at the end of every active Merkle Tree. Child Keys within this window MUST NOT be used for ordinary account transactions and are reserved exclusively for Merkle Tree Rotation.

The size of the Rotation Window is protocol-defined or implementation-dependent. For example, an implementation MAY reserve the final 5% of Child Keys for this purpose.


Rotation Procedure

Wallet software SHOULD continuously monitor the remaining number of available Child Keys.


When the active Merkle Tree enters the Rotation Window, the wallet SHOULD automatically:

· Deterministically generate a new set of Child Keys according to the TRC-102 standard.
· Build a new Merkle Tree.
· Compute the corresponding Merkle Root.
· Create and submit a Merkle Tree Rotation transaction using a valid unused Child Key belonging to the Rotation Window.

This process is intended to occur automatically without requiring user intervention.

Wallet implementations MAY notify the user after a successful Merkle Tree Rotation, but user confirmation is NOT required for the protocol-defined rotation process.


Rotation Validation

Upon receiving a Merkle Tree Rotation transaction, network nodes MUST verify that:

· The transaction signature is valid.
· The signing Child Key belongs to the currently active Merkle Tree.
· The provided Merkle Proof is valid.
· The Child Key belongs to the Rotation Window.
· The Child Key has not been previously consumed.
· The submitted rotation request satisfies all protocol validation rules.

Network nodes MUST reject any ordinary transaction signed by a Child Key belonging to the Rotation Window.


After successful confirmation:

· The stored merkle_root is replaced with the new Merkle Root.
· last_used_child_index is reset to zero.
· The new Merkle Tree becomes the active tree.
· The previous Merkle Tree is permanently deactivated.
· Any remaining unused Child Keys belonging to the previous Merkle Tree become permanently invalid.

Transactions signed by Child Keys belonging to any previously deactivated Merkle Tree MUST be rejected.


Recovery

Because both Access Keys and all Merkle Trees are deterministically derived from the user's master Seed according to the TRC-102 standard, no additional backup material is required.

During account recovery, the wallet regenerates the currently active Merkle Tree from the master Seed and synchronizes its operational state using the merkle_root and last_used_child_index stored in the network State.


Security Properties

The Rotation Window preserves the core OTAK-PQ security model while enabling unlimited long-term account operation.


Specifically:

· Access Keys never participate in signing on-chain transactions.
· No Access Key signature is ever exposed during the rotation process.
· Account ownership remains unchanged.
· Unlimited Child Key generation is supported through successive Merkle Tree Rotations.
· The per-account State size remains constant regardless of the number of rotations performed.
· Merkle Tree replacement is authorized exclusively by valid one-time Child Keys.

By reserving a Rotation Window at the protocol level, OTAK-PQ guarantees that Merkle Tree replacement is enforced by the protocol itself rather than relying solely on wallet implementation behavior.

Consequently, an active Merkle Tree can never become fully exhausted while still retaining sufficient authorization capacity to securely activate its successor.
___
___
# A Distinct Approach to Quantum Threats

Post-Quantum signature algorithms (such as ML-DSA) aim to resist quantum attacks by making the underlying cryptography harder — increasing signature sizes and verification costs. OTAK-PQ takes a fundamentally different approach.

 Rather than strengthening the signature algorithm itself, it eliminates the primary long-term attack surface by ensuring that Access Keys, which control account assets, never publish a signature on the blockchain.

 In other words, post-quantum signatures address quantum threats by hardening cryptography, whereas OTAK-PQ addresses them by eliminating long-term signature exposure.

 This architectural separation helps protect against known quantum attacks, such as Shor's algorithm, while also reducing exposure to future cryptanalytic advances, without requiring any change to the underlying transaction signature algorithm.
___
___
# Threat Model

The core security principles of OTAK-PQ are designed to prevent the exposure of Access Key signatures on the blockchain, thereby limiting the impact of any attack to signatures that are publicly visible.

In the ECDSA signature algorithm, any signature recorded on the blockchain can, in the presence of future computational threats (including quantum computing scenarios), be used as data to recover the private key. Recovering even a single signature gives the attacker access to all assets.

Unlike many similar designs, OTAK-PQ ensures that no Access Key signature is ever exposed on the blockchain – neither during the account bootstrap/activation process nor during normal transaction signing. Therefore, even if a future quantum computer could break the signature of one or more Child Keys, it would still be unable to recover the Access Keys or take control of the account, because:

· No Access Key signature is ever published on the blockchain
· No key list is stored in the network State
· Compromise of one Child Key does not affect other keys
· The relationship between Access Key and Child Key is a one-way function
· Replay attacks are effectively neutralized
· The impact of any possible attack is limited to a single transaction
· The network can validate an unlimited number of Child Keys without storing millions of keys
· Each Child Key is deactivated immediately after use

Consequently, OTAK-PQ shifts the account security model from reliance on long-term keys to a structure based on one-time-use keys, Merkle Proofs, and a Root of Trust.

## The main goal of the OTAK-PQ security model is not to eliminate risk entirely, but rather:

· Limit the impact of any disclosed signature
· Eliminate the reusability of signing keys
· Reduce the attack surface against long-term signature analysis (including quantum threats)
· Transaction signatures are generated only by Child Keys
· Access Keys (Owner/Active Keys) are never directly used to sign on-chain transactions
· Each Child Key is systematically deactivated after use, and only then is its signature published on the network
· Child Keys provide only temporary operational permission to perform a single transaction and are not part of the account’s long-term control structure

Consequently, even if a recorded signature is disclosed:

· The key corresponding to that signature is limited to a past transaction
· No active authority remains for that key to perform a new transaction
· The account’s security control remains at the level of the Root of Trust and the Merkle Root structure recorded for the account

## Analysis of the Impact of Quantum Attacks

Assume an asset transfer transaction is signed with a Child Key:

· The transaction is confirmed by network nodes and the assets arrive at the destination account
· The Child Key is deactivated immediately after confirmation, then the transaction history is recorded on the blockchain and the signature is published

If, in the future, an attacker is able to analyze the recorded signature or recover the corresponding key (even assuming quantum computational capability), this access will be limited solely to a consumed key that:

· Is no longer in an active state on the network
· Cannot sign a new transaction
· No longer has any assets under its control

Therefore, the impact of the attack is limited to the historical level and does not extend to the control level of the account.

## Scope of Security Coverage

OTAK-PQ protects against:

· Reducing exposure of long-term keys on the blockchain
· Limiting attack impact to a single transaction
· Preventing reuse of past signing keys
· Reducing the impact of historical signature analysis in future scenarios

## OTAK-PQ does NOT protect against:

· Theft of Seed Phrase or recovery phrase
· Compromise of the user’s device (malware / keylogger)
· Phishing or social engineering attacks
· Real-time attacks before final transaction confirmation
· Network layer or communication infrastructure attacks
· Risks arising from analysis of transaction signatures recorded before the account migrates to OTAK-PQ

## Comparison of OTAK-PQ with Post-Quantum Algorithms

Post-Quantum algorithms such as CRYSTALS-Dilithium, Falcon, and SPHINCS+ are designed to counter quantum computing threats by making the cryptographic problem harder.

General characteristics of these algorithms:

· Increased signature and key sizes compared to ECDSA
· Increased computational cost of verification in nodes
· Increased memory and bandwidth consumption
· Relative decrease in throughput compared to lighter signatures

In blockchain networks, these costs directly affect TPS, latency, and node resource consumption.

## Impact of OTAK-PQ on Network Speed

OTAK-PQ, instead of increasing cryptographic complexity, focuses on reducing the exposure level of sensitive keys. In this model:

· The underlying signature algorithm (e.g., ECDSA) remains unchanged
· Signature size and transaction structure do not change
· Node processing load remains nearly constant
· No extensive changes to the consensus layer are required

Therefore, OTAK-PQ can act as a complementary security layer, not a replacement for existing signature algorithms.

## Staged Architecture for the Future

OTAK-PQ can act as a transition layer between the current architecture and a possible future migration to Post-Quantum cryptography, especially in current conditions where:

· Computational infrastructure is still limited
· Full migration to heavy PQ algorithms has high operational costs

Adopting OTAK-PQ as a security solution results in:

· Reduced exposure level
· Maintaining network performance without noticeable degradation
·  account structures for future migration
___
___
# Easy migration with OTAK-PQ

In current blockchain architectures, the account identity, public key, and signature algorithm are directly dependent on each other. This dependency makes migrating from current signature algorithms like ECDSA to Post-Quantum algorithms such as:

Falcon
Dilithium
SPHINCS+

a complex and costly process, because:

. The structure of public keys and signatures changes.
. Verification logic must be updated.
. Typically, simultaneous support for multiple algorithms (Hybrid mode) is required.

This can increase node processing load and reduce network efficiency.

## Migration challenges

### 1. In traditional models:
   . The account key is directly dependent on the signature algorithm.
   . Changing the algorithm requires changes at the protocol and network consensus level.
   . Coexistence of multiple algorithms increases operational complexity.
   These factors can lead to:
   . Increased validation latency.
   . Increased node resource consumption.
   . Decreased network throughput.
   . Complexity in the gradual migration process.

### 2. Role of OTAK-PQ in simplifying migration

   In OTAK-PQ, the account structure is designed such that transaction signing operations are separated from the long-term ownership layer of the account.

   The conceptual model is as follows:

   Seed
   ↓
   Access Keys
   ↓
   Merkle Tree
   ↓
   Merkle Root (stored in State)
   ↓
   One-Time Child Keys
   ↓
   Transaction Signatures


In this architecture, Access Keys act as the Root of Trust, and operational transactions are only signed by child keys.
 
### This means:
   . Child keys act as the operational signing layer.
   . Long-term keys (Access Keys) are not used at the on-chain signature level.
   . The signature layer is partially decoupled from the account identity layer.

Reason for facilitated migration in the OTAK-PQ security model:

. This relative decoupling makes it possible to generate child keys with different algorithms in the future.
. The signature layer can be upgraded without changing the core account structure (Seed and Ownership).
. Migration to new algorithms can be performed primarily at the child key layer and transaction signing mechanism, without necessarily requiring fundamental changes to the account ownership model, Seed model, or account recovery process.

For example:

. Current state: Merkle Root based on a set of ECDSA child keys.
. Future: Merkle Root based on a set of Post-Quantum child keys such as Falcon, Dilithium, or other network-approved algorithms.
In both cases, the account ownership model, Bootstrap process, and Seed-based recovery mechanism can remain essentially unchanged.

While:

. The master Seed remains unchanged.
. The account ownership model is preserved.
. The permission structure remains extendable.

## Architectural conclusion

OTAK-PQ, by transferring the responsibility of signing transactions to child keys, enables the creation of a flexible layer for the future evolution of cryptographic algorithms.

This approach can:

. Reduce the direct dependency of an account on a single signature algorithm.
. Simplify the gradual migration path.
. Allow the network to adapt to future algorithms with minimal changes to the core structure.
___
___
# Method for migrating existing accounts to OTAK-PQ after full network deployment

For users who have an active account and a history of outgoing transactions before OTAK-PQ activation, several migration paths with different levels of risk reduction can be defined.

The important point is that signatures recorded on the blockchain are permanent and cannot be deleted after publication. Therefore, any account that had on-chain signature history before OTAK-PQ deployment will always retain part of its cryptographic history.

OTAK-PQ enables significant risk reduction for existing accounts, but the degree of risk reduction is not the same across different migration methods.

## Method One (highest level of risk reduction and recommended method)

### Create a new account with a new seed

In this method, the user generates a new Seed, creates a completely new account, and activates the account.

After activation, assets are transferred from the old account to the new account, and operational use of the old account is stopped.

Advantages of this method:

. No transaction signature history from the old account.
. Complete separation of assets from the old account’s cryptographic history.
. Highest level of risk reduction against long-term threats.

The cost of this method is simply managing and safeguarding the new Seed.

## Method Two (risk reduction without needing a new seed)

### Create a new account from the same seed

In this method, the user uses the same existing Seed and creates a new account via a new derivation path in the TRC-102 standard.

Example path:

m/44'/195'/0'/0/1
The new account has independent public and private keys and can be recovered with the same Seed.

After creating the new account, assets are transferred from the old account to this new account.

Advantages of this method:

. No need to create a new Seed.
. Maintains compatibility with the current backup structure.
. Creates a new key set for future activities.

If the new account has no on-chain signature history before migration and its Bootstrap process is completed according to OTAK-PQ, its exposure to threats based on signature analysis will be significantly lower than that of the original account.

## Method Three (preserving existing account identity)

### Replace the account’s Access Keys

In this method, after transferring assets to the OTAK-PQ structure, the user can, via an AccountPermissionUpdateContract transaction signed by a valid child key and its corresponding Merkle Proof, replace the account’s Access Key set with a new set of Access Keys.

After the changes are recorded, the new Merkle Root corresponding to the new account security structure is stored in the network State, and future transactions will be validated based on the new structure.

This method can be useful for accounts that have a known identifier, activity history, or operational dependencies.

However, it should be noted that:

. Past signature history remains on the blockchain.
. Replacing keys does not erase past cryptographic records.
. This method can reduce some future risks, but it does not turn the account into the equivalent of a newly created account with no on-chain signature history. Because past signature history remains on the blockchain, exposure related to those records will not be completely eliminated, although the account’s future activities will be conducted under the OTAK-PQ security model
