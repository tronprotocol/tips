TIP: XXXX
Title: Native Account Inheritance Mechanism
Authors: Ali (@alichatme), ChatGPT
Status: Draft
Type: Core
Category: Account
Created: 2025-12-29
Discussions-To: https://github.com/tronprotocol/tips/issues/810

Abstract

This TIP proposes a native, optional, protocol-level account inheritance mechanism for the TRON network.
The mechanism allows users to define a time-based inheritance key that can access account assets after a prolonged period of owner inactivity, without revealing private keys, without smart contracts, without additional gas fees, and without dependency on specific wallets or off-chain services.

In addition to inheritance, this mechanism can function as a secure access recovery solution in cases such as permanent loss of seed phrases, cognitive illness, coma, or long-term incapacity.

Motivation

In current blockchain architectures, ownership and access to assets are entirely dependent on possession of private keys.
If the owner experiences any of the following situations:

Death

Long-term unconsciousness or coma

Cognitive diseases (e.g., Alzheimer’s)

Permanent loss or forgetting of the seed phrase or private key

the associated digital assets become permanently inaccessible.

Existing solutions suffer from critical drawbacks:

Sharing seed phrases compromises security

Smart-contract-based inheritance introduces exploit and bug risks

Wallet-based solutions are centralized, non-standard, and non-portable

There is a strong need for a native, protocol-level solution that:

Preserves full owner security during lifetime

Prevents irreversible loss of assets

Avoids legal, technical, or usability complexity

Requires no smart contracts or trust assumptions

Specification
Account Roles

Each TRON account MAY optionally define an additional key role:

Owner Key

Primary account authority

Always valid and active

Inheritance Key

Defined and managed exclusively by the Owner Key

Inactive by default

Becomes valid only after a protocol-defined inactivity condition is met

The Owner Key is never disabled or revoked by inheritance activation.

Inheritance Delay

An optional parameter is stored in the native account state:

inheritance_delay

Minimum: 6 months

Maximum: 240 months (20 years)

This value represents the required duration of owner inactivity before inheritance activation.

Owner Activity Definition

A new native account field is introduced:

last_owner_activity_timestamp

This timestamp MUST be updated when a valid on-chain transaction is executed that:

Is signed by the Owner Key

Results in a verifiable state change

Including, but not limited to:

Asset transfers

Voting

Freeze / unfreeze operations

Staking and unstaking

Reward withdrawal

Direct smart contract invocations signed by the Owner Key

Receiving assets without Owner Key signature MUST NOT update this timestamp.

Inheritance Activation Logic

During transaction signature validation, the protocol evaluates:

(current_time - last_owner_activity_timestamp) >= inheritance_delay

If true, the Inheritance Key is considered valid for transaction authorization.

Activation of the Inheritance Key DOES NOT disable or invalidate the Owner Key.

Behavior After Activation

Once the inheritance condition is met:

The Inheritance Key MAY sign transactions

The Owner Key:

Remains fully valid

MAY reset the inactivity timer

MAY modify the inheritance delay

MAY replace or disable the inheritance key

This design ensures no irreversible or point-of-no-return state is introduced.

Permission Model Integration

The Inheritance Key operates as a restricted authority equivalent to an Active permission, with protocol-enforced limitations.

The Inheritance Key:

MAY initiate asset transfers

MAY stake, unstake, and manage resources

MAY interact with smart contracts

The Inheritance Key MUST NOT:

Modify Owner permissions

Change account permission structure

Replace or revoke the Owner Key

Access or recover private keys or seed phrases

Security Considerations

The mechanism introduces no shared secrets

No private key material is exposed

No smart contracts are involved

All logic is enforced at the consensus/protocol layer

The Owner Key always retains ultimate control

This design minimizes attack surface and eliminates common inheritance exploit vectors.

Transparency

Each transaction MAY include a non-sensitive role identifier:

signature_role: owner
signature_role: inheritance

This allows public auditability and prevents ambiguity without leaking sensitive data.

Wallet UX Considerations

Wallets SHOULD display the following read-only information:

Inheritance feature status (enabled / disabled)

Configured inheritance delay

Remaining time until potential activation

All inheritance configuration is managed as native account metadata and does not require user interaction with gas fees or smart contracts.

Special Scenarios
Long-Term Incapacity

The protocol relies solely on cryptographic inactivity.
A minimum delay of six months provides sufficient protection against accidental activation.

Physical Restriction or Detention

In most scenarios, sending a minimal transaction remains possible.
Failure to do so is interpreted as implicit consent.

Key Loss or Cognitive Decline

The Inheritance Key provides a secure recovery path without compromising owner security.

Backwards Compatibility

Fully optional

No behavior changes for existing accounts

No smart contract dependency

Compatible with existing TRON permission architecture

Conclusion

This TIP introduces a simple yet foundational protocol feature that prevents permanent loss of digital assets on TRON.
By combining security, simplicity, and user sovereignty, native account inheritance can become a defining advantage of the TRON network.
