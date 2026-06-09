TIP: XXXX
Title: Native Account Inheritance Mechanism
Authors: Ali (@alichatme), ChatGPT
Status: Draft
Type: Core
Category: Account
Created: 2025-12-29
Discussions-To: https://github.com/tronprotocol/tips/issues/810

Abstract
This TIP introduces a native, optional, protocol-level inheritance mechanism for all TRON network accounts.
This mechanism allows account owners to define a time-based Inheritance Key for their account, which provides operational access to the account’s assets only if cryptographic inactivity of the Owner Key is detected and after a predefined delay period explicitly set by the owner has elapsed.
The Inheritance Key operates:
Without exposing or compromising the Owner Key
Without relying on smart contracts
Without additional gas or fee requirements
Without dependency on any specific wallet or off-chain service
and is implemented natively at the protocol level as an intrinsic part of TRON accounts.
In addition to inheritance use cases, this mechanism also serves as a secure access recovery path, even for the owner themselves, in situations such as permanent loss of the Seed Phrase, cognitive diseases (e.g., Alzheimer’s), coma, long-term incapacity, or unexpected incidents that prevent access to the primary account key.
Motivation
In current blockchain architectures, ownership and access to assets are entirely dependent on possession of a private key or Seed Phrase.
If any of the following conditions occur:
Death of the owner
Long-term unconsciousness or coma
Memory-related illnesses such as Alzheimer’s
Permanent loss, theft, or destruction of the private key or Seed Phrase
the associated digital assets become permanently and irreversibly inaccessible.
Existing solutions suffer from significant drawbacks:
Sharing a Seed Phrase severely weakens security
Smart contract–based inheritance mechanisms are vulnerable to bugs and exploits
Wallet-based solutions are often centralized, non-standard, and unreliable
Entrusting recovery phrases even to close relatives carries substantial risk
Therefore, the network requires a native protocol-level solution that:
Fully preserves owner security during their lifetime while guaranteeing asset availability for beneficiaries
Prevents irreversible loss of assets
Avoids legal complexity, technical fragility, and poor user experience
Does not rely on smart contracts or trust in third parties
Specification
Account Roles
Every TRON account has an Owner Key that:
Acts as the primary authority of the account
Is always valid and active
This TIP introduces an additional key role:
Inheritance Key
Can only be enabled, disabled, or replaced by the Owner Key
Exists by default for all accounts, but is initially disabled
Has an independent Seed Phrase distinct from the Owner Key
Structurally functions as a time-based Active Permission
The existence of the Inheritance Key at the protocol level is mandatory, while enabling it is entirely optional and requires explicit Owner Key authorization.
Merely configuring the delay and enabling the Inheritance Key does not grant transaction authority until the inactivity condition is fulfilled.
Inheritance Key States
The protocol defines three explicit and auditable states:
1. Disabled
No delay configured
The key is completely inactive at the protocol level
2. Configured
Delay period is defined and signed by the Owner Key
Owner inactivity countdown has started
The key is not yet authorized to sign transactions
3. Active
Owner inactivity condition for the configured delay is satisfied
The Inheritance Key is authorized to sign transactions with Active Permission scope
Activation of the Inheritance Key never disables or restricts the Owner Key.
Explicit Responsibility Separation
Protocol / Network Responsibilities
Maintain the Inheritance Key state and parameters
Enforce activation logic during transaction validation
Apply protocol-level permission restrictions
Record the signer role for each transaction
Wallet Responsibilities
Display Inheritance Key status in read-only mode
Display configured delay period
Display remaining time until activation
Avoid implementing any security logic outside the protocol
User (Owner) Responsibilities
Decide whether to enable or disable inheritance
Configure the delay period
Securely store or distribute the Inheritance Key Seed Phrase to trusted parties
Inheritance Delay
A native account parameter:


inheritance_delay
Minimum: 1 month
Maximum: 240 months (20 years)
Owner Activity Definition
A new native field:


last_owner_activity_timestamp
This value is updated only when:
A transaction is signed by the Owner Key
The transaction causes a verifiable on-chain state change
Including (but not limited to):
Asset transfers
Voting
Freeze / unfreeze operations
Stake / unstake
Reward withdrawal
Voting actions requiring owner authorization
Smart contract interactions
Note: Receiving assets or any activity not signed by the Owner Key does not update this timestamp.
Inheritance Activation Logic
During transaction validation:


(current_time - last_owner_activity_timestamp) >= inheritance_delay
If the condition is satisfied, the Inheritance Key is considered valid for authorization.
Behavior After Activation
The Owner Key retains full control
The Owner may at any time:
Disable the Inheritance Key
Reconfigure the delay and re-enable it
Permanently delete the existing Inheritance Key and replace it with a completely new one
Note: Activation of the Inheritance Key never creates an irreversible or point-of-no-return state.
Permission Model Integration
The Inheritance Key is authorized to:
Transfer assets
Stake, unstake, and manage resources
Vote and claim rewards
Interact with smart contracts
Perform swaps
The Inheritance Key is not authorized to:
Modify Owner permissions
Change the account permission structure
Replace or revoke the Owner Key
Access or recover any Seed Phrase
Security Considerations
There is no shared material between the Owner Key and the Inheritance Key or their Seed Phrases
If an account is accessed via the Inheritance Key, it remains bound to all Owner-defined account settings
No smart contracts are involved
All logic is enforced at the consensus / protocol layer
Delayed Security Layer
Even if the Inheritance Key Seed Phrase is compromised:
No operational access is possible before the Owner inactivity delay expires
This protocol-level delay:
Prevents immediate asset theft
Gives the Owner sufficient time to react and replace the Inheritance Key
This security model is not natively implemented in any existing blockchain.
Transparency
Each transaction may include a non-sensitive signer role identifier:


signature_role: owner
signature_role: inheritance
Wallet UX Considerations
Wallets should support:
Enabling, disabling, configuring delay
Deleting and replacing the Inheritance Key
And display:
Inheritance Key status (Disabled / Configured / Active)
Configured delay period
Remaining time until activation
Automatic timer reset after each Owner Key activity
Backwards Compatibility
Fully optional
No behavior changes for existing accounts
No smart contract dependency
Fully compatible with TRON’s existing permission architecture
Conclusion
This TIP introduces a foundational protocol-level capability that prevents permanent loss of digital assets on the TRON network.
By combining security, predictability, and user sovereignty, native account inheritance can become a strategic and distinguishing advantage for the TRON ecosystem.
