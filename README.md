# TIPs

TRON Improvement Proposals (TIPs) describe standards for the TRON platform, including core protocol specifications, client APIs, and contract standards.

[Gitter](https://gitter.im/tronprotocol/TIPs)  
****

## Contents
 * [TIPs](#tips)
    * [TIPs Guide](#tips-guide)
    * [To Submit a TIP](#to-submit-a-tip)
    * [TIP Status](#tip-status)
    * [TIP Types](#tip-types)
****

## TIPs Guide 
|  ID    | Title  | Author | Type | Hard&nbsp;fork | Status |
|  ----  | ----   | :----:   | :----: | :----:  | :----: |
| TIP&nbsp;01  | [TRON Wallet Proposal](https://github.com/tronprotocol/TIPs/blob/master/tip-01.md)                                       | getty.io| Standards&nbsp;Track |false | -- |
| TIP&nbsp;10  | [TRON Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-10.md)                                        | <zhaohong229@gmail.com> | Standards&nbsp;Track |false | Final |
| TIP&nbsp;12  | [TRON Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-12.md)                              | <jiangyangyang@tron.network> |  Informational |false | Final |
| TIP&nbsp;13  | [Design of TRON account](https://github.com/tronprotocol/TIPs/blob/master/tip-13.md)                                     | <justin@tron.network> | Standards&nbsp;Track   |false | Final |
| TIP&nbsp;16  | [TRON Account Multi-Signature](https://github.com/tronprotocol/TIPs/blob/master/tip-16.md)                               | <zhaohong229@gmail.com> | Core |true | Final |
| TIP&nbsp;17  | [TRON Adaptive Energy Limit Model](https://github.com/tronprotocol/TIPs/blob/master/tip-17.md)                           | <nanfengpo@hotmail.com> |Standards&nbsp;Track |true | Final |
| TIP&nbsp;19  | [Deferred transaction](https://github.com/tronprotocol/tips/blob/master/tip-19.md)                                       | <jiangyangyang@tron.network> | Core |true | Accepted |
| TIP&nbsp;20  | [TRC-20 Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-20.md)                                      |  <zhaohong2292@gmail.com> | Standards&nbsp;Track |true | Final |
| TIP&nbsp;23  | [Add the account world status tree root to the block header](https://github.com/tronprotocol/tips/blob/master/tip-23.md) | <liangzhiyan@tron.network> | Standards&nbsp;Track |true | Accepted |
| TIP&nbsp;24  | [Implement of DB storage with RocksDB](https://github.com/tronprotocol/tips/blob/master/tip-24.md)                       |  <shydesky@gmail.com> | Standards&nbsp;Track |false | Final |
| TIP&nbsp;26  | [Create2](https://github.com/tronprotocol/tips/blob/master/tip-26.md)                                                    |  <jiangxinjian@tron.network>  | VM |false | Final |
| TIP&nbsp;28  | [Built-in Message Queue in Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-28.md)         |  <jiangyangyang@tron.network> | Informational |false | Accepted |
| TIP&nbsp;29  | [Bitwise shifting instructions in Tron](https://github.com/tronprotocol/tips/blob/master/tip-29.md)                      | <jiangxinjian@tron.network> | VM |false | Final |
| TIP&nbsp;30  | [Code hash instructions](https://github.com/tronprotocol/tips/blob/master/tip-30.md)                                     |  <llwslc@gmail.com> | VM |true | Final |
| TIP&nbsp;31  | [Trigger constant contract](https://github.com/tronprotocol/tips/blob/master/tip-31.md)                                  |  <llwslc@gmail.com> | VM |true | Final |
| TIP&nbsp;32  | [Clear the ABI of contract](https://github.com/tronprotocol/tips/blob/master/tip-32.md)                                  |  <llwslc@gmail.com>| VM | true | Final |
| TIP&nbsp;34  | [Event subscribe to support contract without ABI](https://github.com/tronprotocol/tips/blob/tip34/tip-34.md)             |  <wubin1@tron.network> | Standards&nbsp;Track | false | Final |
| TIP&nbsp;37  | [Forbid using TransferContract & TransferAssetContract for contract account](https://github.com/tronprotocol/tips/blob/master/tip-37.md)| <taihao.fu@gmail.com> | VM |true | Final |
| TIP&nbsp;41  | [Optimize transactionHistoryStore occupancy space](https://github.com/tronprotocol/tips/blob/master/tip-41.md)           |  <wubin1@tron.network>| Standards&nbsp;Track |false | Final |
| TIP&nbsp;43  | [Precompiled contract function for signature parallel verification](https://github.com/tronprotocol/tips/blob/master/tip-43.md)| <ksl2945@gmail.com>|Standards&nbsp;Track |true | Final |
| TIP&nbsp;44  | [Address.isContract instructions](https://github.com/tronprotocol/tips/blob/master/tip-44.md)                            | <llwslc@gmail.com> | Standards&nbsp;Track |true | Final |
| TIP&nbsp;51  | [Rate limit of API traffic](https://github.com/tronprotocol/tips/blob/master/tip-51.md)                                  |  <shydesky@gmail.com>| Interface |false | Accepted |
| TIP&nbsp;53  | [Optimize the current TRON delegation mechanism](https://github.com/tronprotocol/tips/blob/master/tip-53.md)|<liangzhiyan@tron.network> | TRC   |true | Final |
| TIP&nbsp;54  | [Automatically active non-existent account when transferring TRX/TRC10 asset in a smart contract](https://github.com/tronprotocol/tips/blob/master/tip-54.md)|  <jiangxinjian@tron.network> | VM | true | Final |
| TIP&nbsp;60  | [Precompiled contract function for multi-signature verification](https://github.com/tronprotocol/tips/blob/master/tip-60.md)|  <ksl2945@gmail.com>| VM |true | Accepted |
****

## To Submit a TIP

Before you submit a TIP, you need to create a issue for comment, and add the issue url to your TIP header.   

1.&nbsp;Fork the repository by clicking "Fork" in the top right.  

2.&nbsp;Add your TIP to your fork of the repository. There is a [TIP template](https://github.com/tronprotocol/TIPs/blob/master/template.md) here.  

3.&nbsp;Submit a Pull Request to TRON's TIPs repository.

Your first PR should be a first draft of the final TIP. It must meet the formatting criteria enforced by the build (largely, correct metadata in the header). An editor will manually review the first PR for a new TIP and assign it a number before merging it. 

Make sure you include a discussions-to header with the URL to a discussion forum or open GitHub issue where people can discuss the TIP as a whole. If a TIP is about the feature development of java-tron, and a PR of the development exists, in your TIP and your java-tron's PR you need to refer each other's github link.

When you believe your TIP is mature and ready to progress past the draft phase, you should do one of two things:

- For a Standards Track TIP of type Core, ask to have your issue added to the agenda of an upcoming All Core Devs meeting, where it can be discussed for inclusion in a future hard fork. If implementers agree to include it, the TIP editors will update the state of your TIP to 'Accepted'.  

- For all other TIPs, open a PR changing the state of your TIP to 'Final'. An editor will review your draft and ask if anyone objects to its being finalized. If the editor decides there is no rough consensus, they may close the PR and request that you fix the issues in the draft before trying again.


## TIP Status

TIPs are separated into a number of status.

- **Draft**: A TIP that is undergoing rapid iteration and changes.  

- **Last Call**: A TIP that is done with its initial iteration and ready for review by a wide audience.  

- **Accepted**: A core TIP that has been in the Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author. The process for Core Devs to decide whether to encode a TIP into their clients as part of a hard fork is not part of the TIP process. If such a decision is made, the TIP will move to the final.  

- **Final (non-Core)**: A TIP that has been in the Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author.  

- **Final (Core)**: A TIP that the Core Devs have decided to implement and release in a future version or has already been released.

- **Active**: If the TIPs are never meant to be completed, the TIPs may have a status of “Active”. 

- **Abandoned**: If a TIP is no longer pursued by the original authors or it may not be a (technically) preferred option anymore.

- **Rejected**: A TIP that is fundamentally broken or a Core TIP that was rejected by the Core Devs and will not be implemented. 

- **Superseded**: A TIP which was previously Final but is no longer considered state-of-the-art. Another TIP will be in the Final status and cite the Superseded TIP. 


## TIP Types

TIPs are separated into a number of types, and each has its own list of TIPs.

* **Standard Track**: Describes any change that affects most or all TRON implementations, such as a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using TRON. Furthermore， Standard TIPs can be broken down into the following categories. 

* **Core**: Improvements requiring a consensus fork, as well as changes that are not necessarily consensus critical but may be relevant to “core dev” discussions.    

* **Networking**: Includes improvements around network protocol.      

* **Interface**: Includes improvements around client API/RPC specifications and standards.    

* **TRC**: Application-level standards and conventions, including contract standards such as token standards (TRC-20).    
* **VM**: Includes improvements around TRON Virtual Machine.    

* **Informational**: Describes a TRON design issue, or provides general guidelines or information to the TRON community, but does not propose a new feature.
