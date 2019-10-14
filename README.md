# TIPs

TRON Improvement Proposals

[Gitter](https://gitter.im/tronprotocol/TIPs)  


## TIPs Guide 
|  ID    | Title  | Author | Type | 
|  ----  | ----   | ----   | ---- | ----  |
| TIP-01  | [TRON Wallet Proposal](https://github.com/tronprotocol/TIPs/blob/master/tip-01.md)                                       | getty.io| Standards Track |
| TIP-10  | [TRON Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-10.md)                                        | <zhaohong229@gmail.com> | Standards Track |
| TIP-12  | [TRON Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-12.md)                              | <jiangyangyang@tron.network> |  Informational |
| TIP-13  | [Design of TRON account](https://github.com/tronprotocol/TIPs/blob/master/tip-13.md)                                     | <justin@tron.network> | Standards Track   |
| TIP-16  | [TRON Account Multi-Signature](https://github.com/tronprotocol/TIPs/blob/master/tip-16.md)                               | <zhaohong229@gmail.com> | Core |
| TIP-17  | [TRON Adaptive Energy Limit Model](https://github.com/tronprotocol/TIPs/blob/master/tip-17.md)                           | <nanfengpo@hotmail.com> |Standards Track |
| TIP-19  | [Deferred transaction](https://github.com/tronprotocol/tips/blob/master/tip-19.md)                                       | <jiangyangyang@tron.network> | Core |
| TIP-20  | [TRC-20 Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-20.md)                                      |  <zhaohong2292@gmail.com> | Standards Track |
| TIP-23  | [Add the account world status tree root to the block header](https://github.com/tronprotocol/tips/blob/master/tip-23.md) | <liangzhiyan@tron.network> | Standards Track |
| TIP-24  | [Implement of DB storage with RocksDB](https://github.com/tronprotocol/tips/blob/master/tip-24.md)                       |  <shydesky@gmail.com> | Standards Track |
| TIP-26  | [Create2](https://github.com/tronprotocol/tips/blob/master/tip-26.md)                                                    |  <jiangxinjian@tron.network>  | VM |
| TIP-28  | [Built-in Message Queue in Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-28.md)         |  <jiangyangyang@tron.network> | Informational |
| TIP-29  | [Bitwise shifting instructions in Tron](https://github.com/tronprotocol/tips/blob/master/tip-29.md)                      | <jiangxinjian@tron.network> | VM |
| TIP-30  | [Code hash instructions](https://github.com/tronprotocol/tips/blob/master/tip-30.md)                                     |  <llwslc@gmail.com> | VM |
| TIP-31  | [Trigger constant contract](https://github.com/tronprotocol/tips/blob/master/tip-31.md)                                  |  <llwslc@gmail.com> | VM |
| TIP-32  | [Clear the ABI of contract](https://github.com/tronprotocol/tips/blob/master/tip-32.md)                                  |  <llwslc@gmail.com>| VM | 
| TIP-34  | [Event subscribe to support contract without ABI](https://github.com/tronprotocol/tips/blob/tip34/tip-34.md)             |  <wubin1@tron.network> | Standards Track | 
| TIP-37  | [Forbid using TransferContract & TransferAssetContract for contract account](https://github.com/tronprotocol/tips/blob/master/tip-37.md)| <taihao.fu@gmail.com> | VM |
| TIP-41  | [Optimize transactionHistoryStore occupancy space](https://github.com/tronprotocol/tips/blob/master/tip-41.md)           |  <wubin1@tron.network>| Standards Track |
| TIP-43  | [Precompiled contract function for signature parallel verification](https://github.com/tronprotocol/tips/blob/master/tip-43.md)| <ksl2945@gmail.com>|Standards Track |
| TIP-44  | [Address.isContract instructions](https://github.com/tronprotocol/tips/blob/master/tip-44.md)                            | <llwslc@gmail.com> | Standards Track |
| TIP-51  | [Rate limit of API traffic](https://github.com/tronprotocol/tips/blob/master/tip-51.md)                                  |  <shydesky@gmail.com>| Interface |
| TIP-53  | [Optimize the current TRON delegation mechanism](https://github.com/tronprotocol/tips/blob/master/tip-53.md)|<liangzhiyan@tron.network> | TRC   |
| TIP-54  | [Automatically active non-existent account when transferring TRX/TRC10 asset in a smart contract](https://github.com/tronprotocol/tips/blob/master/tip-54.md)|  <jiangxinjian@tron.network> | VM | 
| TIP-60  | [Precompiled contract function for multi-signature verification](https://github.com/tronprotocol/tips/blob/master/tip-60.md)|  <ksl2945@gmail.com>| VM |



TRON Improvement Proposals (TIPs) describe standards for the TRON platform, including core protocol specifications, client APIs, and contract standards.

The TIPs repository is [https://github.com/tronprotocol/TIPs](https://github.com/tronprotocol/TIPs)

Before you submit a TIP, you need to create a issue for comment, and add the issue url to your TIP header.   

<h2>To Submit a TIP</h2>

1.&nbsp;Fork the repository by clicking "Fork" in the top right.  

2.&nbsp;Add your TIP to your fork of the repository. There is a [TIP template](https://github.com/tronprotocol/TIPs/blob/master/template.md) here.  

3.&nbsp;Submit a Pull Request to TRON's TIPs repository.   

Your first PR should be a first draft of the final TIP. It must meet the formatting criteria enforced by the build (largely, correct metadata in the header). An editor will manually review the first PR for a new TIP and assign it a number before merging it. Make sure you include a discussions-to header with the URL to a discussion forum or open GitHub issue where people can discuss the TIP as a whole.  

When you believe your TIP is mature and ready to progress past the draft phase, you should do one of two things:

- For a Standards Track TIP of type Core, ask to have your issue added to the agenda of an upcoming All Core Devs meeting, where it can be discussed for inclusion in a future hard fork. If implementers agree to include it, the TIP editors will update the state of your TIP to 'Accepted'.  

- For all other TIPs, open a PR changing the state of your TIP to 'Final'. An editor will review your draft and ask if anyone objects to its being finalised. If the editor decides there is no rough consensus, they may close the PR and request that you fix the issues in the draft before trying again.

<h2>TIP Status</h2>

- **Draft**: A TIP that is undergoing rapid iteration and changes.  

- **Last Call**: A TIP that is done with its initial iteration and ready for review by a wide audience.  

- **Accepted**: A core TIP that has been in Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author. The process for Core Devs to decide whether to encode an TIP into their clients as part of a hard fork is not part of the TIP process. If such a decision is made, the TIP will move to final.  

- **Final (non-Core)**: A TIP that has been in Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author.  

- **Final (Core)**: A TIP that the Core Devs have decided to implement and release in a future version or has already been released.    

<h2>TIP Types</h2>

TIPs are separated into a number of types, and each has its own list of TIPs.

**Standard Track**  

Describes any change that affects most or all TRON implementations, such as a change a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using TRON. Furthermore Standard TIPs can be broken down into the following categories.  

**Core**   

Improvements requiring a consensus fork, as well as changes that are not necessarily consensus critical but may be relevant to “core dev” discussions.    

**Networking**    

Includes improvements around network protocol.      

**Interface**   

Includes improvements around client API/RPC specifications and standards.    

**TRC**  

Application-level standards and conventions, including contract standards such as token standards (TRC-20)    

**VM**  

Includes improvements around TRON Virtual Machine.    

**Informational**  

Describes a TRON design issue, or provides general guidelines or information to the TRON community, but does not propose a new feature.       
