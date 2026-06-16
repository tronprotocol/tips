---
tip: <to be assigned>
title: ASR - Adaptive Secure Recovery
author: Ali (@alichatme)
discussions-to: https://github.com/tronprotocol/tips/issues/858
status: Draft
type: Standards Track
category: Core
created: 2026-05-02
requires:
replaces:
---

ASR – Adaptive Secure Recovery
Adaptive Secure Recovery Standard for Cryptocurrency Accounts


# Introduction

One of the most significant challenges in the cryptocurrency ecosystem is the secure storage of Seed Phrases. Standard protocols like BIP-39, despite their simplicity and widespread adoption, lack any independent cryptographic layer or active defense mechanisms.
Consequently, if the seed phrase is compromised, the user’s entire assets become accessible and transferable without any security barriers. In this context, the ASR standard is introduced to eliminate this fundamental weakness.


# Rationale

ASR is a standard that ensures the user’s digital currency account assets are not at risk, even if the recovery data is lost or stolen.
This is because the recovery process in ASR, in addition to a numerical variable, depends on a private keyword variable. This variable is stored in the user’s memory or in a separate location from the numerical variable and acts as the key for recovery. It consists of only 12 English letters, which are easy to remember or can be stored separately from the numerical variable to ensure that even if the numerical recovery data is fully exposed, recovery without the keyword is practically impossible.

ASR is not a static recovery mechanism; rather, it is a network-dependent, account-state-dependent, and Core security policy-dependent recovery system. This design transforms asset recovery from a single point of failure into a multi-stage, auditable, and adaptive attack-resistant process.


# Overall ASR Architecture
ASR consists of three main components:

. ASR-REC: Recovery Numbers
. ASR-VAR: Variable Secret
. ASR-CRC: Cyclic Reduction Core


## Component One: ASR-REC (Recovery Numbers)
The numerical recovery data, by default, consists of 12 four-digit numbers (a total of 48 digits).
Each number falls within the range 0000 to 9999.
This range operates in a modular manner.
These values are displayed to the user in groups of four digits, separated by - and prefixed with ASR-REC.

### Example of ASR-REC Display Format
ASR-REC-1185-7517-7217-1362-1364-1388-4765-6867-7966-6765-2678-6765

### Display Requirements

· Mandatory Left-to-Right
· Mandatory ASCII
· Mandatory uniform formatting using "-" and displaying ASR-REC to the left of the numerical variable to prevent homography attacks

In the ASR standard, the user can store the ASR-REC digits without concern, because the recovery process, in addition to having ASR-REC, also requires a private lexical variable called ASR-VAR.

## Component Two: ASR-VAR (Variable Secret)
The user’s private variable is a lexical variable consisting of 12 uppercase English letters (A–Z), selected and mapped by the user.
This variable is exclusively held by the user and stored either in the user’s memory or in a location separate from ASR-REC.
ASR-VAR is not stored on the network or in the wallet.
This variable is considered the access key to the assets, and without ASR-VAR, neither the network nor the wallet can map ASR-REC to an account.

### Display Requirements
. Uppercase letters A–Z only
. ASCII encoding only
. No spaces
. Left-to-Right display
. Uniform formatting with "-" with ASR-VAR displayed to the left of the variable to prevent homography attacks
. A maximum of two consecutive repeated letters is allowed

The repetition restriction is applied to prevent the selection of extremely low-entropy variables (e.g., AAAAAAAAAAAA) and is comparable to password policy standards in secure systems.
Allowing up to two consecutive repeated letters ensures linguistic compatibility with natural English language structures.

### Example ASR-VAR Display:
ASR-VAR-SUNBOYINHOME

Each ASR-VAR lexical character, after entering the cryptographic cycle specific to this standard ASR-CRC , is used by default to encrypt four digits of ASR-REC.

## Component Three : ASR-CRC (Cyclic Reduction Core)
This system structurally increases the cost of each guess or attack attempt by creating exponential growth in computational states.

The cyclic cryptographic core is responsible for:
. Converting letters to numbers
. Executing cryptographic cycles via additive variable aggregation to expand numerical digit ranges
. Ensuring full coverage of the numerical range 0000 to 9999 in the default ASR configuration

### Letter-to-Number Mapping
The ASR-VAR vocabulary consists exclusively of uppercase English letters A–Z in ASCII.
Each letter corresponds to a number:
A = 1, B = 2, …, Z = 26

### Cryptographic Cycle Execution:
First, the lexical variables are converted into a numeric sequence, written inside brackets, and separated by -
Then, each variable is added to the next variable in sequence; the last variable is added modularly to the first.
This is performed for all 12 values.
The results are written inside brackets and separated by - forming the next cycle.
With repeated aggregation, subsequent cycles produce numbers with increasing digit lengths.
These cycles continue until the last variable exceeds four digits (in the default ASR configuration).

### Full Range Coverage Guarantee:
Once variable values exceed four digits, only the rightmost four digits of each value are extracted for integration, and the remaining leftmost digits are discarded.
Continuation of the cycles is necessary to guarantee full coverage of the numeric range 0000 to 9999.

### Complete Practical Example of the ASR-CRC Cryptographic Model

Assume the user selects the following ASR-VAR

ASR-VAR-ABCDEFGHIJKL

In the first step, each lexical variable of ASR-VAR is replaced with its numerical digit inside brackets and separated by the - sign.

[1-2-3-4-5-6-7-8-9-10-11-12]

Then, each variable is added to the variable in front of it, and the last variable is also added modularly to the first variable. The results of the additions are written in order inside brackets and separated by the - sign, and recorded as the next cycle.

Numerical example of the first cycle of the above example:

1+2=3  
2+3=5  
3+4=7  
4+5=9  
5+6=11  
6+7=13  
7+8=15  
8+9=17  
9+10=19  
10+11=21  
11+12=23  
12+1=13 

Result:
[3-5-7-9-11-13-15-17-19-21-23-13]

Second Cycle
3+5=8  
5+7=12  
7+9=16  
9+11=20  
11+13=24  
13+15=28  
15+17=32  
17+19=36  
19+21=40  
21+23=44  
23+13=36  
13+3=16 

Result:
[8-12-16-20-24-28-32-36-40-44-36-16]

The cycles continue until the last variable exceeds four digits for all variables. Then, in the above assumption, as well as in the default ASR standard, only the rightmost four digits resulting from the cycle of each variable enter the integration stage, and the remaining left digit(s) of each variable are ignored.

### Modular Integration of ASR-CRC Output with ASR-REC (with Example)

In ASR, the user’s private variable (ASR-VAR) is first processed through the ASR-CRC core.
The output of this process is a four-digit numeric value (ASR-CRC Output), which serves as an intermediate recovery value and cannot independently reconstruct the Seed or private key.
This four-digit value is then modularly added to each four-digit ASR-REC number, and the final result is displayed to the user.
If the sum exceeds 9999, the calculation continues modularly from 0000.

### In another example, with hypothetical numbers different from the previous example.

Assume:
The value of the first four-digit number in ASR-REC is equal to:
4444

And the four-digit output resulting from processing ASR-VAR in the ASR-CRC cycles is equal to:
2222

In this case, the integration is performed as follows:
4444 + 2222 = 6666

The value 6666 is displayed as the ASR-REC value to the user.

### Recovery Process
During recovery, the user enters 6666 as the first ASR-REC value.
After entering ASR-VAR, the wallet reruns ASR-CRC and calculates:
ASR-CRC Output = 2222

The wallet, after subtracting the number resulting from the ASR-CRC cycle from the user's 4-digit ASR-REC number, reconstructs the original middle digit value for account recovery

6666 − 2222 = 4444

Note: If subtraction results in a value below 0000, the calculation proceeds modularly by subtracting from 9999.

After reconstructing ASR-REC values, the wallet sends the recovery proof to the network in accordance with the ASR standard.

If account status, security policies, and timing conditions are approved, the network issues a Network Recovery Authorization (NRA).

Only after receiving this authorization can the recovery process be completed.

This model guarantees that:
Without ASR-VAR, ASR-REC cannot be reconstructed

Even with ASR-REC and ASR-VAR, recovery cannot be completed without network authorization

Recovery requires the simultaneous presence of three independent factors
. ASR-REC
. ASR-VAR
. Network-issued Recovery Authorization

This design transforms recovery from a static operation into a controlled, network-dependent, abuse-resistant process.

## Additional Engineering Considerations and Security Constraints

1. Intentionally Underdetermined Recovery

In ASR, Seed reconstruction is deliberately underdetermined. Even with full possession of ASR-REC and ASR-VAR and complete execution of ASR-CRC, the solution space does not collapse to a single value.
The final degree of mathematical freedom required to determine the Seed is provided exclusively by the network Core and is outside the wallet’s control.

2. Explicit Separation of Local Computation and Final Recovery Control

All cryptographic operations
. ASR-CRC execution
. Recovery Proof generation
. ASR-VAR processing
are performed locally in the wallet.
However, these computations alone never produce the Seed or private key.

Final recovery control depends exclusively on the issuance of Network Recovery Authorization.

3. Fundamental dependence of recovery on network authorization (Network-Gated Recovery)

Completion of the recovery process in ASR is subject to receiving a Network Recovery Authorization (NRA), which:

. Without owner signature
. Without smart contracts
. Without fees or gas
. Only while online

Without NRA, Seed reconstruction is cryptographically and engineering-wise 
impossible.

4. Preventing Adaptive Online Attacks by Stabilizing the Recovery Context

To prevent adaptive online brute-force attacks, the wallet is required to generate a Recovery Context Identifier derived from ASR-REC before any combination of ASR-REC with ASR-VAR and before executing ASR-CRC.

This identifier:

· Is independent of ASR-VAR
· Is independent of variable cryptographic outputs
· Remains constant for all recovery attempts of a single account

Network policies such as rate limits, delays, and attempt counters are applied based on this identifier, not based on the Proof or cryptographic variables.

5. Ineffectiveness of Attacker Variable Changes Changing any of the following does not create a new recovery context:

. ASR-VAR
. Wallet client or version
. IP, VPN, Tor, or network source
. Recovery Proof

All these attempts are mapped to a single Recovery Context and will be subject to network restrictions.

6. Minimum Disclosure Principle During recovery The network, during the recovery process

. Has no access to ASR-VAR
. Does not store Seeds or private keys
. Does not interpret Recovery Proof contents

The network only issues or denies recovery authorization based on account state and security policies.

7. Absolute Prohibition of Offline Recovery

Unlike BIP-39, ASR provides no valid offline recovery path.

Lack of network access definitively prevents recovery.

This is a fundamental design requirement, not an implementation flaw.

8. Deterministic Recovery Context Derivation

To prevent adaptive online brute-force attacks and any attempt to bypass network rate-limiting policies, the wallet is required to generate a unique identifier called the Recovery Context Identifier (RCID) before receiving ASR-VAR from the user and before any cryptographic processing, ASR-CRC execution, or Recovery Proof generation.

This identifier must have the following characteristics:

· Derived deterministically and ONLY from the raw ASR-REC data
· Completely independent of:
  · ASR-VAR
  · ASR-CRC outputs
  · Recovery Proof
  · Wallet version, client, IP, or network conditions
· Remains constant for all recovery attempts associated with a fixed, unchanging ASR-REC
· Generated before any user interaction with the cryptographic process

To state it more explicitly:

RCID must be a function solely of ASR-REC, with no other variable involved in its generation.

Requirement to map all attempts to a single context

The wallet is required to send the generated RCID along with the Network Recovery Authorization (NRA) request to the network.

The network applies all security policies, including:

· Rate Limit
· Delay
· Attempt counters
· Progressive time-based restrictions

based on the RCID, not on cryptographic variables, Proof, or user inputs.

Consequently, changing any of the following by an attacker:

· Changing ASR-VAR
· Changing Recovery Proof
· Changing IP, VPN, Tor, or network source
· Changing wallet/client version or type

will not create a new recovery context.

All such attempts are considered by the network as attempts to recover a single account and will be subject to the same security restrictions.

Security implication of RCID design

This design ensures that an attacker cannot bypass network rate-limiting policies by changing input variables or the execution environment.

As a result:

Adaptive online brute-force attacks in ASR become practically and temporally impossible.

Because the network, instead of rate-limiting "cryptographic attempts", rate-limits the "recovery target".

This pattern, known as account-centric rate limiting, is considered one of the most advanced defense patterns in financial and banking systems.

Implementation MUST

In wallet implementation:

· RCID generation must be performed before receiving any user input and before any cryptographic processing.
· Any dependency of RCID on ASR-VAR, CRC output, Proof, or execution conditions is considered a violation of ASR security requirements.

## Responsibilities

### User Responsibilities
Maintain ASR-VAR and ASR-REC separately

### Wallet Responsibilities
The wallet performs all local cryptographic recovery computations

. Storing ASR-REC
. Receiving and processing ASR-VAR
. Executing ASR-CRC
. Generating Recovery Proof

However, the wallet is deliberately designed to lack the ability to independently reconstruct the Seed or derive the private key.
Even with correct and complete execution of all local steps, the recovery process will not converge to a single value without receiving the additional data issued by the Core network.

The wallet:

· Is not the owner of the Seed
· Does not have final control over the account
· Cannot complete recovery offline or unilaterally

This limitation is a fundamental security constraint in the ASR design, not an implementation flaw.

### Role and Responsibilities of the Core Network in the ASR Recovery Process

The Core network in ASR does not act as a "computing engine" or "Seed holder". Instead, it is responsible for providing the final degree of freedom necessary to complete the recovery.

Network responsibilities are limited to the following:

· Evaluating account status and active security policies
· Applying rate limits, delays, and attempt counters based on the Recovery Context
· Issuing or denying the Network Recovery Authorization (NRA)

The network:

· Has no access to ASR-VAR
· Does not store or reconstruct the Seed or private key
· Does not participate in the wallet's local cryptographic computations

However, without issuing the NRA, the Seed reconstruction process is cryptographically and engineering-wise impossible to complete.
This dependency is not an ownership control mechanism, but a network‑centric security constraint to prevent unauthorized recovery and adaptive attacks.

### ASR Network Layer Responsibilities

. No smart contracts
. No gas or fees
. Core logic level
· First block of 3 unsuccessful attempts → Apply a 24-hour restriction.
· Each subsequent block of 3 unsuccessful attempts → Apply a time restriction double the previous one (e.g., 24h → 48h → 96h → ...).
· Mandatory: When a restriction is applied, a countdown timer must be displayed to the user, indicating the remaining waiting time.


# Delayed Account Activation Option

When viewing recovery data, the user can enable the Delayed Account Activation option (disabled by default).  
The user can select a delay period from 1 to 94 days and register it with the owner’s signature on the network.

If this option is enabled, whenever a **Network Recovery Authorization (NRA)** is issued by the network and account recovery succeeds, the newly recovered account will remain inactive until the end of the delay period.

**Displaying Recovered Devices with a Single RCID and the Ability to Terminate Previous Sessions:**
- It should be possible to view active and inactive devices associated with an RCID, as well as to terminate previous sessions for ASR accounts.
- **Limitation for newly recovered accounts:** A newly recovered account will not be able to terminate previous sessions for 30 days after activation.

**Status during the delay period:**  
- Assets are view‑only.  
- No signed operations by the owner are permitted before the delay ends.  
- A countdown timer shows the remaining time to the user.  
- Notifications are sent to previously active wallets.

**Security note:**  
If the owner still has access to a previously active wallet, they can, upon detecting suspicious activity or a potential attack, stop the new account activation process before the delay ends by providing a valid signature.

### Definition of “Owner Activity”
Any valid on-chain transaction signed by the owner that changes network state, including but not limited to

. Asset transfers
. Voting
. Freeze/unfreeze
. Stake/unstake
. Reward withdrawal
. Direct smart contract calls

Receiving assets without owner signature is not considered activity.

## Position of ASR in the Key Generation to Recovery Chain (Engineering Placement of ASR)

To accurately understand the ASR standard, it is necessary to clearly define its position in the engineering chain from cryptographic key generation to the account recovery process.

In HD wallet architecture and the BIP-39 standard, the key generation path is as follows:

Entropy
→ Checksum
→ Mnemonic (2048 words)
→ PBKDF2-HMAC-SHA512
→ 512-bit Seed
→ Master Private Key
→ Public Key / Address
→ Wallet
→ Recovery using Mnemonic

In this structure, the Mnemonic directly represents the Seed, and anyone who gains access to it can recover the user's private key and assets without any security barrier.

Where ASR Fits in This Chain

The ASR standard does not change any of the following processes:

· Entropy generation
· Seed generation
· Key Derivation Functions (KDF)
· Private and public key generation
· HD Wallet structure
· Network cryptographic algorithms

All of the above steps remain exactly as before, following existing cryptographic standards.

ASR only redefines the Recovery layer.

From an engineering perspective, the new chain will be as follows:

Entropy
→ Seed Generation (unchanged)
→ Master Keys (unchanged)
→ Wallet (unchanged)

↓ (at recovery time)

ASR Recovery Layer
    ASR-REC (numeric recovery data)
    ASR-VAR (user private variable)
    ASR-CRC (cyclic cryptographic process)
    Network Verification

Fundamental Difference from BIP-39

In BIP-39:
Mnemonic = Seed = Access to Private Key

In ASR:
ASR-REC ≠ Seed
ASR-REC has no relation to the Seed or private key without ASR-VAR.
ASR-REC is only an "input to the recovery process", not a direct representation of the private key.

The recovery process is only completed when:

1. The user enters ASR-REC
2. The user enters ASR-VAR
3. The ASR-CRC cryptographic cycle is executed
4. The network verifies the process

Without these four steps, recovery is impossible.

## Checksum in ASR
The Checksum in the ASR standard is used solely to detect typographical errors in the recovery data entered by the user and has no security or cryptographic role in the recovery process.

The Checksum is generated as a value derived from the ASR-REC data using the SHA-512/256 function, but this value:

· Does not by itself indicate the correctness of ASR-REC
· Does not enable full or definitive validation of the recovery data
· Does not reduce the cryptographic search space

Final validation of recovery data in ASR is inherently network‑dependent and occurs only within the framework of the online recovery process, after verification of account status and Core network security policies.

Consequently:

· The Checksum in ASR is merely a user‑experience aid
· It provides no valid path for offline verification of recovery data
· It does not enable recovery or validation independent of the network in any way

## Role of KDF and Seed in ASR

The Key Derivation Function (KDF) and Seed are still generated before ASR.

ASR has no involvement in Seed generation whatsoever.

Rather, after Seed generation and wallet creation, the recovery data – instead of a Mnemonic – is defined in the form of ASR-REC and dependent on ASR-VAR.

In engineering terms:

ASR replaces the Mnemonic, not the Seed.

### Engineering Conclusion

ASR is not a key generation standard.

ASR is a Secure Recovery Standard that:

· Without changing core network cryptography
· Without changing key algorithms
· Without relying on smart contracts
· Without fees

transforms the recovery layer from a single point of failure into a multi-stage, network-dependent process.

This precise positioning introduces ASR as an independent, complementary layer in cryptographic wallet architecture, not a replacement for key generation standards.


# Absolute Prohibition of Offline Recovery in ASR

Unlike BIP-39, where recovery is completely offline, ASR is fundamentally designed to be network‑dependent.

Executing ASR-CRC and mapping to ASR-REC alone does not result in the reconstruction of the Seed or private key.
The output of all ASR components is only an intermediate recovery value.

Full recovery is conditional upon receiving a Network Recovery Authorization (NRA) from the Core network.

In the absence of NRA, recovery is engineering‑wise impossible.


# Threat Model
The ASR standard is designed to protect the account recovery process against threats related to the disclosure of recovery data, and not to counter full compromise of the user's execution environment.

1. ASR is resilient against:

· Partial or full disclosure of recovery data (ASR-REC)
· Disclosure of the user's private variable (ASR-VAR)
· Theft of physical or digital backups
· Offline brute‑force attacks (fundamentally impossible)
· Adaptive online brute‑force attacks (using Recovery Context and rate limiting)
· Phishing attacks targeting the recovery process
· Shoulder surfing
· Attempts to recover without network authorization
· Malicious delayed recovery, even in the event of simultaneous theft of all recovery data
    (using Recovery Delay, network notifications, and account‑state dependency)

2. Out of Scope:

· Active malware with simultaneous access to the user's execution environment
· Compromise of operating system, firmware, or runtime
· Attacks based on full device control at the time of owner signing
· Non‑cryptographic attacks such as physical coercion or in‑person social engineering


# Why ASR Is a Recovery Alternative to BIP-39 (Design Rationale)

BIP-39 is a Seed generation standard that makes recovery dependent on full knowledge of the Mnemonic.
In this model, recovery is a completely offline, unsupervised process with no distinction between the legitimate owner and an attacker.

In contrast, ASR does not replace the Seed or private key.
Instead, it transforms the recovery process into a conditional, multi‑stage, network‑dependent flow.

The key differences are:

· In BIP‑39, full disclosure of the Mnemonic directly leads to loss of assets.
    In ASR, the recovery data alone is incapable of recovery and is useless without network approval.
· BIP‑39 enables offline brute‑force attacks and unlimited attempts without rate limiting.
    ASR fundamentally makes this class of attacks impossible by eliminating offline recovery.
· BIP‑39 has no native concept of "recovery control, suspension, or rejection."
    ASR turns recovery into an observable, rate‑limit‑able, and policy‑governable event at the network level.
· BIP‑39 reduces recovery to a single point of failure.
    ASR eliminates this single point of failure by separating ASR‑REC, ASR‑VAR, and network verification cycles.
· In BIP‑39, the network is unaware of the recovery process.
    In ASR, the network is part of the recovery security model.

As a result, ASR enhances security not by replacing basic cryptography, but by completely redesigning the concept of digital asset recovery.


# Summary
ASR is not a recovery phrase; it is a security‑oriented, network‑dependent recovery system.

In this standard, the recovery process is deliberately underdetermined, and even with full possession of the user's recovery data, reconstructing the Seed or controlling the assets is impossible without a recovery authorization issued by the network.

By moving recovery from a single point of failure to a multi‑stage process that depends on account status, time, and the Core network's security policies, ASR completely eliminates offline recovery while enabling monitoring, rate limiting, delays, and resistance to adaptive attacks.

This design transforms asset recovery from a static, uncontrollable operation into a dynamic, manageable, and abuse‑resistant mechanism.
