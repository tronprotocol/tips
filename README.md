🧠 TIP-796: TRON Account-Layer Username Standard (with “TR” Prefix)

Title: TRON Account-Layer Username Standard with Uppercase “TR” Prefix
Status: Draft
Type: Standards Track
Authors: Ali & ChatGPT
GitHub: @alichatme
Created: September 25, 2025
License: MIT License – 2025


---

📘 Summary

This proposal introduces a native username standard for TRON accounts, implemented directly at the Account Layer —
requiring no smart contracts, gas, or Layer 2 integration.

Each username is unique, permanent, and non-transferable.
The system is designed to improve human readability, reduce transfer errors caused by address copy/paste mistakes, and prevent phishing or address spoofing attacks — while remaining fully compatible with the existing TRON network architecture.


---

🧩 Username Structure

All TRON usernames must begin with the uppercase prefix TR,
followed by lowercase English letters (a–z) and digits (0–9) in one of the following three modes:

Mode 1: TR + two English words + a four-digit number

Example: TRsunboy1185


Mode 2: TR + two English words with a four-digit number placed in between

Example: TRsun7217boy


Mode 3: TR + a four-digit number + two English words

Example: TR7516sunboy


> Rule: No special characters, spaces, or underscores are allowed.
The TR prefix clearly identifies the TRON network and provides a consistent, universal naming pattern across all languages and systems.




---

🔠 LTR Requirement (Left-to-Right)

All usernames must be stored and displayed Left-to-Right (LTR)
and use only the permitted characters described above.

This requirement prevents Homograph attacks and visual confusion in Right-to-Left (RTL) languages such as Persian or Arabic.


---

⚙️ Core Rules

Prefix: The uppercase TR prefix is mandatory and part of the username itself.

Case Sensitivity: Must follow the rule above — TR always uppercase; other letters always lowercase.

Wallet Display: Wallets must show both the full username (including TR) and the complete address before confirming a transaction.

No Shortening: Wallets must not remove or hide the TR prefix.

No Smart Contracts: This system operates entirely at the Account Layer and does not affect fees, gas, or network validation.



---

📊 Capacity and Namespace

With approximately 650,000 meaningful English words,
this design supports over 12.6 quadrillion (12,600,000,000,000,000) unique usernames —
providing a vast namespace for assigning TRON account identifiers.


---

🎯 Objective

To establish a native, decentralized, and reliable username system at the Account Layer,
without dependence on off-chain naming services, Layer 2 systems, or any gas or fee consumption.

This standard enhances user experience, strengthens protection against address spoofing,
and ensures accurate fund delivery across the TRON ecosystem.


---

🔮 Future Extensions

Possible future updates may include:

Additional username format modes

Extended character sets

Special identifiers for categories such as NFTs, MemeCoins, and other on-chain projects


Any such updates will be reviewed and approved by the TRON Core Development Team.


---

📄 License

MIT License – 2025
Open-source for all TRON developers.


---

🔗 Related Discussion

GitHub Issue: #799

Official Pull Request: #803
