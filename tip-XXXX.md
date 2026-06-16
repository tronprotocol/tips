---
TIP: XXXX
Title: Native Account Inheritance Mechanism
Authors: Ali (@alichatme)
Status: Draft
Type: Core
Category: Account
Created: 2025-12-29
Discussions-To: https://github.com/tronprotocol/tips/issues/810
---
# Abstract

This TIP introduces a native, optional, protocol-level inheritance mechanism for TRON accounts.

Under this proposal, every TRON account is capable of supporting a dedicated Inheritance Key at the protocol level. The Inheritance Key is disabled by default and becomes operational only if explicitly configured by the account owner.

The owner may configure an inheritance delay period and assign an Inheritance Key. If no valid Owner Key activity occurs during the configured delay period, the Inheritance Key becomes active and may operate within the scope of a restricted Active Permission.

### The Owner Key always remains the ultimate authority of the account. At any time, including after inheritance activation, the owner may:

. Disable the Inheritance Key

. Modify or reset the inheritance delay

. Replace the existing Inheritance Key with a completely new one

Activation of the Inheritance Key never disables, replaces, or reduces the authority of the Owner Key.

### The inheritance mechanism operates:

. Without exposing or sharing the Owner Key

. Without relying on smart contracts

. Without dependency on any specific wallet implementation

. Without dependency on off-chain services

Configuration, activation, deactivation, and replacement of the Inheritance Key are native protocol-level account operations and do not require deployment of smart contracts or any inheritance-specific fees.

Transactions executed through an active Inheritance Key remain subject to TRON's normal bandwidth, energy, and fee rules.

Beyond inheritance scenarios, this mechanism can also function as a secure recovery path for account owners in situations such as loss of private keys, loss of seed phrases, cognitive impairment, long-term incapacity, or other events that prevent access to the primary account credentials.


# Rationale

Designing a native inheritance mechanism at the protocol level, rather than relying on smart contracts or off-chain solutions, is the result of a deliberate trade-off analysis between security, usability, decentralization, and prevention of irreversible asset loss.

## 1. Why Protocol-Level Instead of Smart Contracts?

Smart contract–based inheritance solutions suffer from fundamental limitations:

. Vulnerability to bugs and upgrades:
Smart contracts can be hacked, and malicious upgrades can bypass inheritance logic.

· Gas dependency: Activation requires the beneficiary to pay gas – which may be impossible if the beneficiary lacks sufficient TRX.

· No native permission integration:
Smart contracts cannot distinguish between true Owner Key inactivity versus simple non-use of a specific contract.

· Incomplete access to consensus truth: Smart contracts intentionally do not have access to the full, consensus-verifiable history of Owner Key activity (votes, freezes, permission updates, governance actions). This is a deliberate VM security property, not an implementation flaw.

By implementing inheritance natively in the TRON protocol, all accounts automatically possess the potential for inheritance, and activation carries zero additional gas overhead.

## 2. Why Not Key Sharing or Multi-Signature?

· Sharing Seed Phrase: Irreversibly compromises security. A trusted party could access assets at any time without delay.

· Multi-signature: This is a mechanism for simultaneous trust distribution, not time-based recovery. The owner must permanently grant signing power to other parties from day one, which means loss of exclusive control.

The proposed model ensures that during the owner's active lifetime, the Inheritance Key provides zero access, preserving full unilateral control.

## 3. Rationale for the Time-Based Delay Model

The delay period (minimum 1 month, maximum 20 years) serves two critical security functions:

. Detection window: If the Inheritance Key Seed Phrase is compromised, the delay gives the owner time to react before any theft can occur.

. Proof of true inactivity: Short delays risk premature activation during travel or temporary disengagement, causing false inheritance events.
The 1-month minimum balances practical usability (beneficiaries do not wait indefinitely) with security (no immediate post-loss exploitation).

## 4. Delayed Security Layer Against Inheritance Key Seed Exposure

Even if the Inheritance Key Seed Phrase is exposed, no operational access is possible before the inactivity delay expires. This is a native protocol-level security layer not implemented in any other blockchain.

## 5. Why No Smart Contract Involvement in the Permission Model?

Restricting the Inheritance Key from modifying Owner permissions or account structure is a deliberate design choice to preserve Owner Sovereignty. Even after the Inheritance Key becomes active:

· The owner retains full ability to disable inheritance.
· The owner can reclaim exclusive control at any time.

This prevents a "hostile inheritance" scenario where a beneficiary could lock out a returning owner.

## 6. Comparison with Other Blockchains

No major Layer 1 blockchain (Bitcoin, Ethereum, Solana, BNB Chain, or TRON itself) currently implements a native, protocol-level, time-delayed inheritance mechanism with independent key material. Existing approaches are either centralized, legal wills (unenforceable on-chain), or vulnerable to smart contract hacks.

This TIP positions TRON as a first mover in solving the permanent asset loss problem without compromising self-custody.

## 7. Why the Inheritance Key Seed Must Be Independent from the Owner Key

If the Inheritance Key were derived from the Owner Key, compromising the Owner Key would simultaneously compromise inheritance security. By maintaining fully independent seed phrases:

· No mathematical relationship exists between the two keys.

· The owner can rotate or replace the Inheritance Key without changing the Owner Key.

· Even if the Inheritance Key is leaked, the owner's day-to-day assets remain safe during the delay period.

## 8. Protocol Necessity (Response to "Why Must This Be at Protocol Layer")

The necessity lies in this reality: "The last valid activity of the Owner Key is a consensus fact, not a reliable application-level signal." No smart contract can deterministically and safely verify:

· Whether the Owner Key has truly been inactive

· Whether activity occurred outside the contract (vote, freeze, permission update)

· Whether a transaction was actually signed by the Owner Key or by another Active Permission

Smart contracts intentionally lack access to this level of information – this is a VM security feature, not a flaw. Consequently, any smart contract–based solution will inevitably suffer from either:

· False positives (incorrect activation),

· False negatives (failure to activate when needed),

· Or reliance on off-chain assumptions.

Therefore, this capability sits exactly at the boundary of what the protocol must define – neither above nor below.

## 9. Protocol Maintenance Cost and Complexity

This proposal:

· Introduces no new signature paths

· Grants no new power to any key

· Adds only a conditional check inside existing signature validation

· Is fully optional and disabled by default

Its maintenance and complexity profile remains at the level of existing permission primitives (Owner/Active, multi-signature), not at the level of behavioral policy systems.

## 10. Handling Edge Cases: Owner Returns After Activation

The specification explicitly allows the owner to:

· Disable the Inheritance Key

· Reconfigure the delay period

· Replace the Inheritance Key entirely

No irreversible state is created – even after activation.

## 11. Rationale for Updating last_owner_activity_timestamp

The "last_owner_activity_timestamp" is updated only when a transaction meets all of the following criteria:

. Successfully authorized through the account's Owner Permission,
. Successfully passes protocol validation requirements,
. Executes successfully and results in a committed on-chain state change.

This definition intentionally excludes:

· Failed or reverted transactions, even when authorized through the Owner Permission, because they do not produce a committed state change.

· Execution failures, VM exceptions, contract reverts, resource exhaustion failures (e.g., OUT_OF_ENERGY), insufficient balance failures, and any other transactions that do not result in a committed state change.

· Read-only calls (e.g., view/pure functions), because they do not alter state.

· Transactions rejected during protocol validation, including invalid signatures, malformed transactions, or authorization failures.

· Passive events, such as receiving assets, because they do not demonstrate owner intent or awareness.

Rationale for this strict definition:

· Preventing trivial resets: If failed transactions, passive receipts, or non-state-changing operations updated the timestamp, inheritance could be postponed indefinitely, defeating the mechanism's purpose.

· Consensus alignment: Only successful state-changing transactions provide an unambiguous, verifiable proof of owner activity that all consensus participants can independently verify.

· Security: This ensures that the inactivity condition reflects genuine owner absence rather than accidental activity, failed execution attempts, or automated interactions that do not represent meaningful owner participation.

By keeping the definition narrow and deterministic, the protocol maintains a clear, auditable, and consensus-safe boundary for what constitutes "Owner activity."

## 12. Interaction with Existing Permission System and Multi-Signature

The Inheritance Key is designed as a time-conditioned Active Permission and is fully integrated into TRON's existing permission architecture.

· Active Permissions: The Inheritance Key reuses the existing Active Permission structure. No new PermissionType is introduced.

· Multi-Signature Compatibility: Existing multi-signature behavior and validation rules remain unchanged. The inheritance mechanism does not modify or bypass any existing multisig security model.

· Owner Supremacy: Owner Permission always remains the highest authority. The Owner may disable, reconfigure, or replace the Inheritance Key at any time, including after activation.

This design ensures that the inheritance mechanism remains fully compatible with TRON's existing permission framework while preserving all current security guarantees.

## 13. Inheritance Key as an Extension of the Existing Permission System

This proposal does not introduce a separate account-control path.

· Structurally, the Inheritance Key is implemented as a standard Active Permission already supported by TRON accounts.

· The only addition occurs at the protocol validation layer, where a time-based condition determines whether this specific Active Permission is currently authorized.

· Existing permission attributes, including weights, thresholds, and operation scopes, remain fully applicable.

As a result, the inheritance mechanism extends the existing permission architecture rather than introducing a parallel authorization model.

## 14. Simultaneous Owner and Inheritance Transactions in the Same Block

If Owner-authorized and Inheritance-authorized transactions appear within the same block:

· Standard deterministic transaction execution rules defined by the TRON protocol apply.

· The transaction processed first determines the resulting account state for subsequent transactions within that block.

· No inheritance-specific ordering rules are introduced.

This approach preserves protocol simplicity, predictability, and compatibility with existing multi-key account behavior.

## 15. Fee and Resource Clarification: Configuration vs. Transaction Execution

A distinction must be made between inheritance configuration and transaction execution.

· Configuration, activation, deactivation, replacement, or delay-period updates of the Inheritance Key are native account-management operations and do not require any inheritance-specific fees, smart-contract deployment costs, or additional protocol charges beyond standard protocol account-management behavior.

· However, any transaction submitted through an active Inheritance Key consumes normal TRON resources, including bandwidth, energy, and applicable transaction fees, exactly as any other Active Permission transaction.

This distinction is important: the inheritance mechanism itself introduces no additional operational cost, while all on-chain actions performed through the Inheritance Key continue to follow TRON's standard resource and fee model.


# Motivation

In current blockchain architectures, ownership and access to assets are entirely dependent on possession of a private key or Seed Phrase.

If any of the following conditions occur:

. Death of the owner
. Long-term unconsciousness or coma
. Memory-related illnesses such as Alzheimer’s
. Permanent loss, theft, or destruction of the private key or Seed Phrase

the associated digital assets become permanently and irreversibly inaccessible.

Existing solutions suffer from significant drawbacks:

. Sharing a Seed Phrase severely weakens security
. Smart contract–based inheritance mechanisms are vulnerable to bugs and exploits
. Wallet-based solutions are often centralized, non-standard, and unreliable
. Entrusting recovery phrases even to close relatives carries substantial risk

Therefore, the network requires a native protocol-level solution that:

. Fully preserves owner security during their lifetime while guaranteeing asset availability for beneficiaries
. Prevents irreversible loss of assets
. Avoids legal complexity, technical fragility, and poor user experience
. Does not rely on smart contracts or trust in third parties


# Specification

## Account Roles

Every TRON account has an Owner Key that:

. Acts as the primary authority of the account
. Is always valid and active

## This TIP introduces an additional key role:

Inheritance Key

. Can only be enabled, disabled, or replaced by the Owner Key
. Exists by default for all accounts, but is initially disabled
. Has an independent Seed Phrase distinct from the Owner Key
. Structurally functions as a time-based Active Permission

The existence of the Inheritance Key at the protocol level is mandatory, while enabling it is entirely optional and requires explicit Owner Key authorization.

Merely configuring the delay and enabling the Inheritance Key does not grant transaction authority until the inactivity condition is fulfilled.

## Inheritance Key States

The protocol defines three explicit and auditable states:

1. Disabled

No delay configured
The key is completely inactive at the protocol level

2. Configured Delay

period is defined and signed by the Owner Key
Owner inactivity countdown has started
The key is not yet authorized to sign transactions

3. Active

. Owner inactivity condition for the configured delay is satisfied
. The Inheritance Key is authorized to sign transactions with Active Permission scope
. Activation of the Inheritance Key never disables or restricts the Owner Key.


# Explicit Responsibility Separation

## Protocol / Network Responsibilities

. Maintain the Inheritance Key state and parameters
. Enforce activation logic during transaction validation
. Apply protocol-level permission restrictions
. Record the signer role for each transaction

## Wallet Responsibilities

. Display Inheritance Key status in read-only mode
. Display configured delay period
. Display remaining time until activation
. Avoid implementing any security logic outside the protocol

## User (Owner) Responsibilities

. Decide whether to enable or disable inheritance
. Configure the delay period
. Securely store or distribute the Inheritance Key Seed Phrase to trusted parties
Inheritance Delay

### A native account parameter:

. inheritance_delay
Minimum: 1 month
Maximum: 240 months (20 years)

## Owner Activity Definition

A new native field:
last_owner_activity_timestamp

### This value is updated only when:

. A transaction is signed by the Owner Key
. The transaction causes a verifiable on-chain state change

### Including (but not limited to):

. Asset transfers
. Voting
. Freeze / unfreeze operations
. Stake / unstake
. Reward withdrawal
. Voting actions requiring owner authorization
. Smart contract interactions

Note: Receiving assets or any activity not signed by the Owner Key does not update this timestamp.

### Inheritance Activation Logic

During transaction validation:

(current_time - last_owner_activity_timestamp) >= inheritance_delay

If the condition is satisfied, the Inheritance Key is considered valid for authorization.

### Behavior After Activation

. The Owner Key retains full control

### The Owner may at any time:

. Disable the Inheritance Key
. Reconfigure the delay and re-enable it
. Permanently delete the existing Inheritance Key and replace it with a completely new one

Note: Activation of the Inheritance Key never creates an irreversible or point-of-no-return state.

### Permission Model Integration

The Inheritance Key is authorized to:

. Transfer assets
. Stake, unstake, and manage resources
. Vote and claim rewards
. Interact with smart contracts
Perform swaps

### The Inheritance Key is not authorized to:

. Modify Owner permissions
. Change the account permission structure
. Replace or revoke the Owner Key
. Access or recover any Seed Phrase


# Security Considerations

There is no shared material between the Owner Key and the Inheritance Key or their Seed Phrases

## If an account is accessed via the Inheritance Key

. it remains bound to all Owner-defined account settings
. No smart contracts are involved
. All logic is enforced at the consensus / protocol layer

## Delayed Security Layer

Even if the Inheritance Key Seed Phrase is compromised:

No operational access is possible before the Owner inactivity delay expires

### This protocol-level delay:

. Prevents immediate asset theft
. Gives the Owner sufficient time to react and replace the Inheritance Key

This security model is not natively implemented in any existing blockchain.

## Transparency

Each transaction may include a non-sensitive signer role identifier:

signature_role: owner

signature_role: inheritance

## Wallet UX Considerations

Wallets should support:

Enabling, disabling, configuring delay
Deleting and replacing the Inheritance Key
And display:

. Inheritance Key status (Disabled / Configured / Active)
. Configured delay period
. Remaining time until activation
. Automatic timer reset after each Owner Key activity

## Backwards Compatibility

. Fully optional
. No behavior changes for existing accounts
. No smart contract dependency
. Fully compatible with TRON’s existing permission architecture

## Conclusion

This TIP introduces a foundational protocol-level capability that prevents permanent loss of digital assets on the TRON network.

By combining security, predictability, and user sovereignty, native account inheritance can become a strategic and distinguishing advantage for the TRON ecosystem.
