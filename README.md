# TIPs

Tron Improvement Proposals

[gitter](https://gitter.im/tronprotocol/TIPs)  


## Tips Guide 
|  ID   | Title  |
|  ----  | ----  |
| Tip-01  | [TRON Wallet Proposal](https://github.com/tronprotocol/TIPs/blob/master/tip-01.md)                                       |
| Tip-10  | [TRON Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-10.md)                                        |
| Tip-12  | [TRON Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-12.md)                              |
| Tip-13  | [Design of TRON account](https://github.com/tronprotocol/TIPs/blob/master/tip-13.md)                                     |
| Tip-16  | [TRON Account Multi-Signature](https://github.com/tronprotocol/TIPs/blob/master/tip-16.md)                               |
| Tip-17  | [TRON Adaptive Energy Limit Model](https://github.com/tronprotocol/TIPs/blob/master/tip-17.md)                           |
| Tip-19  | [Deferred transaction](https://github.com/tronprotocol/tips/blob/master/tip-19.md)                                       |
| Tip-20  | [TRC-20 Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-20.md)                                      |
| Tip-23  | [Add the account world status tree root to the block header](https://github.com/tronprotocol/tips/blob/master/tip-23.md) |
| Tip-24  | [Implement of DB storage with RocksDB](https://github.com/tronprotocol/tips/blob/master/tip-24.md)                       |
| Tip-26  | [Create2](https://github.com/tronprotocol/tips/blob/master/tip-26.md)                                                    |
| Tip-28  | [Built-in Message Queue in Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-28.md)         |
| Tip-29  | [Bitwise shifting instructions in Tron](https://github.com/tronprotocol/tips/blob/master/tip-29.md)                      |
| Tip-30  | [Code hash instructions](https://github.com/tronprotocol/tips/blob/master/tip-30.md)                                     |
| Tip-31  | [Trigger constant contract](https://github.com/tronprotocol/tips/blob/master/tip-31.md)                                  |
| Tip-32  | [Clear the ABI of contract](https://github.com/tronprotocol/tips/blob/master/tip-32.md)                                  |
| Tip-34  | [Event subscribe to support contract without ABI](https://github.com/tronprotocol/tips/blob/tip34/tip-34.md)             |
| Tip-37  | [Forbid using TransferContract & TransferAssetContract  for contract account](https://github.com/tronprotocol/tips/blob/master/tip-37.md)|
| Tip-41  | [Optimize transactionHistoryStore occupancy space](https://github.com/tronprotocol/tips/blob/master/tip-41.md)           |
| Tip-43  | [Precompiled contract function for signature parallel verification](https://github.com/tronprotocol/tips/blob/master/tip-43.md)|
| Tip-44  | [Address.isContract instructions](https://github.com/tronprotocol/tips/blob/master/tip-44.md)                            |
| Tip-51  | [Rate limit of API traffic](https://github.com/tronprotocol/tips/blob/master/tip-51.md)                                  |
| Tip-54  | [Automatically active non-existent account when transferring TRX/TRC10 asset in a smart contract](https://github.com/tronprotocol/tips/blob/master/tip-54.md)|
| Tip-60  | [Precompiled contract function for multi-signature verification](https://github.com/tronprotocol/tips/blob/master/tip-60.md)|

 




TRON Improvement Proposals (TIPs) describe standards for the TRON platform, including core protocol specifications, client APIs, and contract standards.

The TIPS repository is [https://github.com/tronprotocol/TIPs](https://github.com/tronprotocol/TIPs)


<h2> To Submit a TRC </h2>
1.Before create a TIP, you need to create a new TRC in the TIPS’ issue.
2.Follow the template to fill the content and name the title with the format like: TRC-200: Create Key. 
Here is the template: https://github.com/tronprotocol/tips/blob/master/template.md
3.If your issues are to solve the existed TIPs' problems, figure out the TIPs' file address in the TRC.
4.Submit the TRC.

The TRC is the first step to be submitted before you submit the TIP. The TRC should follow the format of the criteria enforced by the build (largely, correct metadata in the header). Make sure you open GitHub issue where people can discuss the TRC as a whole.

If anyone have no more questions about the TRC after discussion, next step is to submit a TIP. When you submit the TIP, conclude the discussion and fill the template in detail. Make sure the TIP lists the discussion address of the TRC.

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
