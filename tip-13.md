```
tip: 13
title: Account System Standard
author: Justin Sun(@justintron) <justin@tron.network> 
discussions to: https://github.com/tronprotocol/TIPs/issues/13
status: Final
type: Standards Track
category: TRC
created: 2018-12-21
```

## Simple Summary

This doc describes the design of the TRON account system.

## Abstract

Account system mainly including account name spec, account name exchange, transfer through account name. Account name will be equal to Address but easier memorize.
TRX can only transfer by address.

## Motivation

the address is the unique identity of an account.
It's very normal for people who familiar with Bitcoin, but It's not very friendly to people who never used bitcoin or other crypto coins and the address is too long for the user to read and write. Using address to represent account stops people to try to use TRON. Every account should have a name and the name is equal to the address.

## Specification
###Account Name

`length: [8, 20]
case sensitive: No`

**how to set account name**
The address is sha256(public_key) in TRON. after the address is activated through transfer user get an account in the network. The user can set the account name to this address by RPC interface. something like below:

```
Account {

string account_name; // lovelycat

string address1;    // prim address

string address2;  

}
```
if I send TRX to the lovelycat, that means I send TRX to address 1.
###Account Auth
###Account Exchange

the account name can be traded through muti-sig.

```
Account {                                                           
string account_name; // lovelycat                        
string address1;    // prim address   =>                  
string address2;                                                     
}      

Account {                                                           
string account_name; // lovelycat                        
string address3;    // prim address                
string address4;                                                     
} 
```

That means account lovelycat controlled by adderss3 and address4.

## Reserved List

The full note should keep a reserved list for famous company and brand. All the SR can manager this list by voting the proposal to add or remove name from list.
