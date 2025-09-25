TIP: <to be assigned>  
Title: Native Username System for TRON Accounts  
Author: <Your Name or GitHub handle>  
Status: Draft  
Created: 2025-09-25  

## Abstract  
This proposal introduces a **native username system** for TRON blockchain accounts. Each account may register a unique human-readable username, reducing the risk of misdirected transactions caused by complex alphanumeric addresses. The system will be implemented at the protocol level to ensure universality across wallets, exchanges, and dApps.  

## Motivation  
One of the main usability issues in blockchain networks is the reliance on long, complex addresses (e.g., `TXY9uZs...`). Sending assets to an incorrect address due to copy-paste errors or mistyped characters can result in permanent loss of funds.  

By allowing TRON users to register a **unique username**, the network becomes more user-friendly, more secure, and more attractive to both individuals and businesses. Similar systems have proven successful in Web2 (social usernames, email handles) and in Web3 (ENS, etc.), but TRON lacks a native, protocol-level solution.  

## Specification  

### Username Registration  
- Each TRON account may register a single unique username.  
- Usernames are case-insensitive and must be unique across the network.  
- Once registered, a username cannot be deleted.  

### Change Policy  
- A registered username may only be changed **once per year**.  
- This balances flexibility with protection against abuse and impersonation.  

### Length and Availability Rules  
- **8 characters or more**: open to individuals. These usernames are non-tradable and permanently bound to the account.  
- **7 characters or fewer**: reserved for companies, institutions, and brands. These usernames may be transferable and can be reserved officially via TRON DAO.  

### Corporate Reservations  
- Companies and verified organizations can reserve short usernames (≤7 characters).  
- TRON DAO manages the reservation process.  
- Payments may be made in **installments over 1 year**, making it accessible to both startups and enterprises.  

### Protocol-Level Integration  
- Username mapping will be implemented **natively** within the TRON blockchain, not as an external contract.  
- Wallets, exchanges, and dApps should display both the username and the underlying TRON address when making transfers.  

## Rationale  
- **Security**: Reduces misdirected transfers caused by complex addresses.  
- **Adoption**: Simplifies user onboarding and encourages mainstream adoption.  
- **Brand Protection**: Companies can secure official usernames, preventing fraud and phishing.  
- **Governance**: TRON DAO manages corporate reservations, ensuring fairness and transparency.  

## Governance  
- TRON DAO will oversee and govern the allocation of corporate usernames (≤7 characters).  
- Community voting may be used to decide pricing models, installment options, and dispute resolution.  
- Individuals’ usernames (≥8 characters) remain fully decentralized and non-transferable.  

## Backward Compatibility  
- No changes to existing TRON addresses.  
- Addresses remain the core identifier at the protocol level.  
- Usernames act as a human-readable overlay.  

## Implementation  
- Requires protocol-level update to support account-to-username mapping.  
- Wallets, exchanges, and dApps will need to implement display and search functionality for usernames.  
