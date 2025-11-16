🧠 TIP-796 — TRON Account-Layer Username Standard (With Mandatory “TR” Prefix)
Status: Draft
Type: Standards Track
Authors: Ali & ChatGPT
GitHub: @alichatme
Created: September 25, 2025
License: MIT — 2025
📘 Summary
TIP-796 introduces a native, human-readable, non-transferable username standard implemented directly at the Account Layer of the TRON blockchain.
This system:
Requires no smart contracts
Requires no gas or fees
Attaches the username automatically and permanently to the account
Eliminates all major address-related attack vectors
Remains fully compatible with the existing TRON architecture
TIP-796 establishes a secure and spoof-proof identity layer that dramatically reduces user mistakes, prevents phishing, and protects users against modern Web3 attack methods.
🧩 Username Structure
All TRON usernames must begin with the uppercase prefix TR, followed by lowercase English letters (a–z) and digits (0–9) in one of the three allowed modes:
Mode 1
TR + two lowercase words + four digits
Example: TRsunboy1185
Mode 2
TR + word + four digits + word
Example: TRsun7217boy
Mode 3
TR + four digits + two lowercase words
Example: TR7516sunboy
Rules
No special characters, no spaces, no underscores
Strictly ASCII-only (a–z + 0–9)
Strict LTR (Left-to-Right) storage & display
The uppercase TR prefix is mandatory and part of the username identity
🔠 LTR Enforcement & Anti-Spoofing Protection
All usernames are stored and displayed using strict Left-to-Right (LTR) directionality.
This eliminates:
Homograph attacks
RTL/LTR bidirectional text exploits
Visual spoofing in Persian/Arabic/Hebrew
Font-based manipulation
⚙️ Core Rules
The TR prefix is required and cannot be hidden or omitted.
Wallets must display the full username and full address before signing.
Wallets must not shorten, collapse, or hide any part of the username.
System operates fully at the Account Layer — no fees, no contracts, no L2 required.
🔥 Complete Attack Coverage — Why TIP-796 Provides the Highest Security Level in Web3
TIP-796 is the only naming standard designed to neutralize every major address-layer attack currently seen across blockchain networks.
1. Clipboard Hijacking
Malware replaces the copied address ➜ Username mismatch instantly reveals it.
2. Address Spoofing / Look-Alike Address Generation
Attackers generate thousands of similar addresses ➜ Username is impossible to imitate.
3. Homograph Attacks
Using similar-looking Unicode characters ➜ ASCII-only usernames block this completely.
4. RTL/LTR Visual Reversal Attacks
Bidirectional text exploits (common in Persian/Arabic/Hebrew) ➜ LTR-only eliminates them fully.
5. UI-Layer Manipulation (Phishing Wallets)
Fake wallets hide or reorder parts of the address ➜ Username must be displayed fully before signing.
6. Social Engineering Attacks
Humans verify names, not hex strings ➜ A clear username prevents human error.
7. Spam Activation & Transaction Pollution
Attackers send micro-transactions to appear in your history ➜ Username makes spoof attempts ineffective.
Result:
TIP-796 is the first blockchain username standard that neutralizes all seven categories of Web3 address-based attacks.
🔥 Username Assignment — Anti-Bot & Anti-Abuse Measures
To prevent bot farms, mass wallet creation, automated harvesting of names, or username farming, TIP-796 introduces the following optional but recommended mechanisms:
1. Cooldown Window (Recommended Default: 24 hours)
The username is assigned only after a configurable waiting period after account activation.
Network operators may increase this to 48 hours or more if needed.
This makes large-scale automated farming impractical.
2. Minimum Balance Requirement
A username is assigned only if the account holds a minimum balance during the cooldown period.
Suggested default: 2 TRX (or higher, e.g., 10 TRX, if stronger protection is desired).
This makes mass wallet creation economically non-viable.
3. Wallet Onboarding Confirmation
Before showing the username, wallets must require the user to:
Scroll through a multilingual explanation
Confirm understanding via a checkbox
Review: 
How usernames work
How they protect users
How they prevent phishing
This significantly reduces phishing and user-errors.
4. Local Anti-Bot Challenge (Optional)
Wallets may implement:
Local lightweight PoW
CAPTCHA / anti-automation challenge
The network only verifies, but does not execute, the challenge.
Combined effect:
Bots must:
Wait 24–48 hours
Deposit real TRX
Solve onboarding
Solve anti-automation
=> Attack becomes economically impossible.
📊 Namespace Capacity
Using >650,000 English words, TIP-796 supports over:
12.6 quadrillion unique usernames
More than enough for centuries of TRON expansion.
🎯 Goal
Create a native, decentralized, zero-cost, spoof-proof identity layer
that protects users from all currently known Web3 address-based attacks — without L2, without ENS-like contracts, and without gas fees.
🔮 Future Enhancements
Possible extensions include:
Additional username formats
Extended character sets
Special categories for NFTs, MemeCoins, dApps, and system accounts
📄 License
MIT — 2025
🔗 References
Primary Issue: #799
Updated Pull Request: #803
