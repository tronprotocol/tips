# TIPs

TRON Improvement Proposals (TIPs) describe standards for the TRON platform, including core protocol specifications, client APIs, and contract standards.

****

## Contents
- [TIPs](#tips)
  - [Contents](#contents)
  - [TIPs Guide](#tips-guide)
  - [To Submit a TIP](#to-submit-a-tip)
  - [TIP Status](#tip-status)
  - [TIP Types](#tip-types)
****

## TIPs Guide 

| ID            | Title                                                                                                                                                         |             Author             |         Type         |  Category  | Hard&nbsp;fork |  Status   |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------:|:--------------------:|:----------:|:--------------:|:---------:|
| TIP&nbsp;10   | [TRON Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-10.md)                                                                             |    <zhaohong229@gmail.com>     | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;12   | [TRON Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-12.md)                                                                   |  <jiangyangyang@tron.network>  |    Informational     |    TRC     |     false      |   Final   |
| TIP&nbsp;13   | [Design of TRON account](https://github.com/tronprotocol/TIPs/blob/master/tip-13.md)                                                                          |     <justin@tron.network>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;16   | [TRON Account Multi-Signature](https://github.com/tronprotocol/TIPs/blob/master/tip-16.md)                                                                    |    <zhaohong229@gmail.com>     | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;17   | [TRON Adaptive Energy Limit Model](https://github.com/tronprotocol/TIPs/blob/master/tip-17.md)                                                                |    <nanfengpo@hotmail.com>     | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;19   | [TRC-19 Deferred transaction](https://github.com/tronprotocol/TIPs/blob/master/tip-19.md)                                                                     |  <jiangyangyang@tron.network>  | Standards&nbsp;Track |    Core    |      true      | Deferred  |
| TIP&nbsp;20   | [TRC-20 Token Standard](https://github.com/tronprotocol/TIPs/blob/master/tip-20.md)                                                                           |    <zhaohong2292@gmail.com>    | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;23   | [Add the account world status tree root to the block header](https://github.com/tronprotocol/tips/blob/master/tip-23.md)                                      |   <liangzhiyan@tron.network>   | Standards&nbsp;Track |    Core    |      true      | Accepted  |
| TIP&nbsp;24   | [Implement of DB storage with RocksDB](https://github.com/tronprotocol/tips/blob/master/tip-24.md)                                                            |      <shydesky@gmail.com>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;26   | [Create2](https://github.com/tronprotocol/tips/blob/master/tip-26.md)                                                                                         |  <jiangxinjian@tron.network>   | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;28   | [Built-in Message Queue in Event Subscription Model](https://github.com/tronprotocol/TIPs/blob/master/tip-28.md)                                              |  <jiangyangyang@tron.network>  |    Informational     |            |     false      |   Final   |
| TIP&nbsp;29   | [Bitwise shifting instructions in Tron](https://github.com/tronprotocol/tips/blob/master/tip-29.md)                                                           |  <jiangxinjian@tron.network>   | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;30   | [Code hash instructions](https://github.com/tronprotocol/tips/blob/master/tip-30.md)                                                                          |       <llwslc@gmail.com>       | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;31   | [Trigger constant contract](https://github.com/tronprotocol/tips/blob/master/tip-31.md)                                                                       |       <llwslc@gmail.com>       | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;32   | [Clear the ABI of contract](https://github.com/tronprotocol/tips/blob/master/tip-32.md)                                                                       |       <llwslc@gmail.com>       | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;37   | [Forbid using TransferContract & TransferAssetContract for contract account](https://github.com/tronprotocol/tips/blob/master/tip-37.md)                      |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;41   | [Optimize transactionHistoryStore occupancy space](https://github.com/tronprotocol/tips/blob/master/tip-41.md)                                                |     <wubin1@tron.network>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;43   | [Precompiled contract function for signature parallel verification](https://github.com/tronprotocol/tips/blob/master/tip-43.md)                               |      <ksl2945@gmail.com>       | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;44   | [Address.isContract instructions](https://github.com/tronprotocol/tips/blob/master/tip-44.md)                                                                 |       <llwslc@gmail.com>       | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;51   | [Rate limit of API traffic](https://github.com/tronprotocol/tips/blob/master/tip-51.md)                                                                       |      <shydesky@gmail.com>      | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;53   | [Optimize the current TRON delegation mechanism](https://github.com/tronprotocol/tips/blob/master/tip-53.md)                                                  |   <liangzhiyan@tron.network>   | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;54   | [Automatically active non-existent account when transferring TRX/TRC10 asset in a smart contract](https://github.com/tronprotocol/tips/blob/master/tip-54.md) |  <jiangxinjian@tron.network>   | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;60   | [Precompiled contract function for multi-signature verification](https://github.com/tronprotocol/tips/blob/master/tip-60.md)                                  |      <ksl2945@gmail.com>       | Standards&nbsp;Track |     VM     |      true      | Accepted  |
| TIP&nbsp;62   | [Tron consensus algorithm introduction](https://github.com/tronprotocol/tips/blob/master/tip-62.md)                                                           |      <xing@tron.network>       | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;64   | [Tron tron mix consensus Analytics](https://github.com/tronprotocol/tips/blob/master/tip-64.md)                                                               |      <xing@tron.network>       | Standards&nbsp;Track |    Core    |     false      |   Draft   |
| TIP&nbsp;101  | [Wallet Keystore Specification](https://github.com/tronprotocol/tips/blob/master/tip-101.md)                                                                  |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |     false      | Last Call |
| TIP&nbsp;102  | [Hierarchical Deterministic Wallet](https://github.com/tronprotocol/tips/blob/master/tip-102.md)                                                              |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |     false      | Last Call |
| TIP&nbsp;104  | [Data Signing Specification](https://github.com/tronprotocol/tips/blob/master/tip-104.md)                                                                     |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |     false      | Last Call |
| TIP&nbsp;105  | [Multi-signature Permission Operation](https://github.com/tronprotocol/tips/blob/master/tip-105.md)                                                           |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;120  | [ECDSA Signature Encoding Specification](https://github.com/tronprotocol/tips/blob/master/tip-120.md)                                                         |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |     false      |   Final   |
| TIP&nbsp;127  | [Support Tron-DEX based on system contracts](https://github.com/tronprotocol/tips/blob/master/tip-127.md)                                                     |    <liu.sean@tron.network>     | Standards&nbsp;Track |    CORE    |     false      |   Draft   |
| TIP&nbsp;128  | [TIP128 Lite Fullnode support](https://github.com/tronprotocol/tips/blob/master/tip-128.md)                                                                   |     <ray.wu@tron.network>      | Standards&nbsp;Track |    CORE    |     false      |   Draft   |
| TIP&nbsp;135  | [Shielded TRC-20 Contract](https://github.com/tronprotocol/tips/blob/master/tip-135.md)                                                                       |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |     false      |   Final   |
| TIP&nbsp;137  | [Zero-knowledge Proof Verification functions](https://github.com/tronprotocol/tips/blob/master/tip-137.md)                                                    |  <federico.zhen@tron.network>  | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;138  | [Pedersen hash function](https://github.com/tronprotocol/tips/blob/master/tip-138.md)                                                                         |  <federico.zhen@tron.network>  | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;156  | [Vote instructions in TVM](https://github.com/tronprotocol/tips/blob/master/tip-156.md)                                                                       |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      | Withdrawn |
| TIP&nbsp;157  | [Freeze instructions in TVM](https://github.com/tronprotocol/tips/blob/master/tip-157.md)                                                                     |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;165  | [TRC-165 Standard Interface Detection In Contract](https://github.com/tronprotocol/tips/blob/master/tip-165.md)                                               | <timothychungkitwai@gmail.com> | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;171  | [STAKE instructions in TVM](https://github.com/tronprotocol/tips/blob/master/tip-171.md)                                                                      |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      | Withdrawn |
| TIP&nbsp;174  | [CHAINID instructions in TVM](https://github.com/tronprotocol/tips/blob/master/tip-174.md)                                                                    |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;175  | [SELFBALANCE instructions in TVM](https://github.com/tronprotocol/tips/blob/master/tip-175.md)                                                                |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;176  | [altbn128 operation energy reduction in TVM](https://github.com/tronprotocol/tips/blob/master/tip-176.md)                                                     |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;178  | [TOKENISSUE and UPDATEASSET Instruction in TVM](https://github.com/tronprotocol/tips/blob/master/tip-178.md)                                                  |     <taihao.fu@gmail.com>      | Standards&nbsp;Track |     VM     |      true      | Withdrawn |
| TIP&nbsp;191  | [Signed Data Standard](https://github.com/tronprotocol/tips/blob/master/tip-191.md)                                                                           |     <yanghang8612@163.com>     | Standards&nbsp;Track |    TRC     |     false      |   Final   |
| TIP&nbsp;196  | [Reward SRs with the transaction fees charged for bandwidth and Energy](https://github.com/tronprotocol/tips/blob/master/tip-196.md)                          |    <liu.sean@tron.network>     | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;204  | [Make MAX_FEE_LIMIT configurable as a chain property](https://github.com/tronprotocol/tips/blob/master/tip-204.md)                                            |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;207  | [A proposal to improve network resources model ](https://github.com/tronprotocol/tips/blob/master/tip-207.md)                                                 |    <liu.sean@tron.network>     | Standards&nbsp;Track |    Core    |      true      |   Draft   |
| TIP&nbsp;209  | [Adapt to Solidity 0.6.0](https://github.com/tronprotocol/tips/blob/master/tip-209.md)                                                                        |    <neo.hong@tron.network>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;222  | [Improve transaction execution speed](https://github.com/tronprotocol/tips/blob/master/tip-222.md)                                                            |   <kiven.liang@tron.network>   | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;250  | [Include transaction results on the chain](https://github.com/tronprotocol/tips/blob/master/tip-250.md)                                                       |   <andy.zhang@tron.network>    | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;268  | [SmartContract ABI optimization](https://github.com/tronprotocol/tips/blob/master/tip-268.md)                                                                 |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;269  | [Optimize the performance of block processing](https://github.com/tronprotocol/tips/blob/master/tip-269.md)                                                   |      <forfreeday@163.com>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;271  | [Vote for SR in Smart Contract](https://github.com/tronprotocol/tips/blob/master/tip-271.md)                                                                  |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;272  | [Compatible with EVM](https://github.com/tronprotocol/tips/blob/master/tip-272.md)                                                                            |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;276  | [Optimize block verification logic](https://github.com/tronprotocol/tips/blob/master/tip-276.md)                                                              |    <lucas.wu@tron.network>     | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;281  | [Optimize the query of database](https://github.com/tronprotocol/tips/blob/master/tip-281.md)                                                                 |      <forfreeday@163.com>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;285  | [Node startup optimization](https://github.com/tronprotocol/tips/blob/master/tip-285.md)                                                                      |    <lucas.wu@tron.network>     | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;289  | [Block Broadcast Optimization](https://github.com/tronprotocol/tips/blob/master/tip-289.md)                                                                   |    <lucas.wu@tron.network>     | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;290  | [Dynamic store optimization](https://github.com/tronprotocol/tips/blob/master/tip-290.md)                                                                     |    <lucas.wu@tron.network>     | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;292  | [Add a proposal to adjust the free net limit in an account](https://github.com/tronprotocol/tips/blob/master/tip-292.md)                                      |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;293  | [Add a proposal to adjust the total net limit](https://github.com/tronprotocol/tips/blob/master/tip-293.md)                                                   |  <federico.zhen@tron.network>  | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;295  | [Optimize assets of account](https://github.com/tronprotocol/tips/blob/master/tip-295.md)                                                                     |      <forfreeday@163.com>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;298  | [Reformat manifest](https://github.com/tronprotocol/tips/blob/master/tip-298.md)                                                                              |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;306  | [Adapt to solidity_0.8.4](https://github.com/tronprotocol/tips/blob/master/tip-306.md)                                                                        |    <neo.hong@tron.network>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;318  | [Adapt to Ethereum London Upgrade](https://github.com/tronprotocol/tips/blob/master/tip-318.md)                                                               |    <neo.hong@tron.network>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;343  | [DB params optimization ](https://github.com/tronprotocol/tips/blob/master/tip-343.md)                                                                        |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Draft   |
| TIP&nbsp;344  | [Optimize instruction execution for TVM](https://github.com/tronprotocol/tips/blob/master/tip-344.md)                                                         |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |     false      |   Final   |
| TIP&nbsp;362  | [Optimized node broadcast data caching](https://github.com/tronprotocol/tips/blob/master/tip-362.md)                                                          |      <forfreeday@163.com>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;366  | [Node startup optimization](https://github.com/tronprotocol/tips/blob/master/tip-366.md)                                                                      |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;369  | [Node support prometheus metrics](https://github.com/tronprotocol/tips/blob/master/tip-369.md)                                                                |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;370  | [Node support conditionalized stop](https://github.com/tronprotocol/tips/blob/master/tip-370.md)                                                              |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;382  | [TIP-382: Optimize the data structure of account assets](https://github.com/tronprotocol/tips/blob/master/tip-382.md)                                         |       <wb_bupt@163.com>        | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;383  | [TIP-383: Optimize transaction cache loading](https://github.com/tronprotocol/tips/blob/master/tip-383.md)                                                    |       <wb_bupt@163.com>        | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;387  | [TIP-387: Transaction memo fee](https://github.com/tronprotocol/tips/blob/master/tip-387.md)                                                                  |        <jell7@163.com>         | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;388  | [TIP-388: Optimize light node synchronization logic](https://github.com/tronprotocol/tips/blob/master/tip-388.md)                                             |       <wb_bupt@163.com>        | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;391  | [TIP-391: Optimize fetch block process](https://github.com/tronprotocol/tips/blob/master/tip-391.md)                                                          |      <vikingzzu@163.com>       | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;397  | [Raise limit of the 13th network parameter](https://github.com/tronprotocol/tips/blob/master/tip-397.md)                                                      |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;425  | [TIP-425: Speed up TCP connection establishment](https://github.com/tronprotocol/tips/blob/master/tip-425.md)                                                 |       <wb_bupt@163.com>        | Standards&nbsp;Track |    Net     |     false      |   Final   |
| TIP&nbsp;428  | [TIP-428: Increase the probability that the block processing thread acquires the lock](https://github.com/tronprotocol/tips/blob/master/tip-428.md)           |       <wb_bupt@163.com>        | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;440  | [Transaction cache optimization](https://github.com/tronprotocol/tips/blob/master/tip-440.md)                                                                 |        <jell7@163.com>         | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;461  | [Optimize data consistency for system abnormals](https://github.com/tronprotocol/tips/blob/master/tip-461.md)                                                 |     <ray.wu@tron.network>      | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;465  | [New reward calculation algorithm](https://github.com/tronprotocol/tips/blob/master/tip-465.md)                                                               |       <bladehan@163.com>       | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;467  | [Stake 2.0 - A new TRON stake model](https://github.com/tronprotocol/tips/blob/master/tip-467.md)                                                             |       <lxcmyf@gmail.com>       | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;474  | [Optimize the return value of chainid opcode](https://github.com/tronprotocol/tips/blob/master/tip-474.md)                                                    |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;476  | [Delegate Data Structure Optimization](https://github.com/tronprotocol/tips/blob/master/tip-476.md)                                                           |       <lxcmyf@gmail.com>       | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;491  | [Dynamic Energy Model](https://github.com/tronprotocol/tips/blob/master/tip-491.md)                                                                           |   <daniel.cao@tron.network>    | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;534  | [Remove Vulnerable APIs](https://github.com/tronprotocol/tips/blob/master/tip-534.md)                                                                         |    <halibobo1205@gmail.com>    | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;541  | [Support canceling unstaking in Stake 2.0](https://github.com/tronprotocol/tips/blob/master/tip-541.md)                                                       |       <lxcmyf@gmail.com>       | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;542  | [Resource delegating supports customizable lock period](https://github.com/tronprotocol/tips/blob/master/tip-542.md)                                          |       <lxcmyf@gmail.com>       | Standards&nbsp;Track |    Core    |      true      |   Final   |
| TIP&nbsp;543  | [Implement EIP-3855 PUSH0 instruction](https://github.com/tronprotocol/tips/blob/master/tip-543.md)                                                           |     <yanghang8612@163.com>     | Standards&nbsp;Track |     VM     |      true      |   Final   |
| TIP&nbsp;544  | [Add `data` to the http interfaces interacting with smart contract](https://github.com/tronprotocol/tips/blob/master/tip-544.md)                         |     <yanghang8612@163.com>     | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;547  | [Connection precheck before P2P communication](https://github.com/tronprotocol/tips/blob/master/tip-547.md)                                                   |       <wb_bupt@163.com>        | Standards&nbsp;Track | Networking |     false      |   Final   |
| TIP&nbsp;548  | [Node Discovery via DNS](https://github.com/tronprotocol/tips/blob/master/tip-548.md)                                                                         |       <317787106@qq.com>       | Standards&nbsp;Track | Networking |     false      |   Final   |
| TIP&nbsp;549  | [P2P support IPv6 protocol](https://github.com/tronprotocol/tips/blob/master/tip-549.md)                                                                      |       <317787106@qq.com>       | Standards&nbsp;Track | Networking |     false      |   Final   |
| TIP&nbsp;550  | [P2P message snappy compression](https://github.com/tronprotocol/tips/blob/master/tip-550.md)                                                                 |   <allen.cheng@tron.network>   | Standards&nbsp;Track | Networking |     false      |   Final   |
| TIP&nbsp;555  | [Network upgrade logic optimization](https://github.com/tronprotocol/tips/blob/master/tip-555.md)                                                             |   <allen.cheng@tron.network>   | Standards&nbsp;Track |    Core    |     false      |   Final   |
| TIP&nbsp;712  | [TRON typed structured data hashing and signing](https://github.com/tronprotocol/tips/blob/master/tip-712.md)                                                 |     <yanghang8612@163.com>     | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;721  | [TRC-721 Non-Fungible Token Standard](https://github.com/tronprotocol/tips/blob/master/tip-721.md)                                                            | <timothychungkitwai@gmail.com> | Standards&nbsp;Track |    TRC     |      true      |   Final   |
| TIP&nbsp;1102 | [TIP-1102: Opt-in account exposure](https://github.com/tronprotocol/tips/blob/master/tip-1102.md)                                                             |    <aaronluotron@gmail.com>    | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;1155 | [Multi Token Standard](https://github.com/tronprotocol/tips/blob/master/tip-1155.md)                                                                          |     <yanghang8612@163.com>     | Standards&nbsp;Track |    TRC     |     false      |   Final   |
| TIP&nbsp;1193 | [TIP-1193: TRON Provider JavaScript API](https://github.com/tronprotocol/tips/blob/master/tip-1193.md)                                                        |    <aaronluotron@gmail.com>    | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;3326 | [TIP-3326: Wallet Switch TRON Chain Method](https://github.com/tronprotocol/tips/blob/master/tip-3326.md)                                                     |    <aaronluotron@gmail.com>    | Standards&nbsp;Track | Interface  |     false      |   Final   |
| TIP&nbsp;4906 | [TRC-4906: Fork from ERC-4907 Rental NFT](https://github.com/tronprotocol/tips/blob/master/tip-4906.md)                                                     |    <lopeed_prcy>    | Standards&nbsp;Track | TRC  |     false      |   Final   |

****

## To Submit a TIP

Before you submit a TIP, you need to create an issue for comment and add the issue URL to your TIP header.   

1.&nbsp;Fork the repository by clicking "Fork" in the top right.  

2.&nbsp;Add your TIP to your fork of the repository. There is a [TIP template](https://github.com/tronprotocol/TIPs/blob/master/template.md) here.  

3.&nbsp;Submit a Pull Request to TRON's TIPs repository.

Your first PR should be a first draft of the final TIP. It must meet the formatting criteria enforced by the build (largely, correct metadata in the header). An editor will manually review the first PR for a new TIP and assign it a number before merging it. 

Make sure you include a discussions-to header with the URL to a discussion forum or open GitHub issue where people can discuss the TIP as a whole. If a TIP is about the feature development of java-tron, and a PR of the development exists, in your TIP and your java-tron's PR you need to refer each other's github link.

When you believe your TIP is mature and ready to progress past the draft phase, you should do one of two things:

- For a Standards Track TIP of type Core, ask to have your issue added to the agenda of an upcoming All Core Devs meeting, where it can be discussed for inclusion in a future hard fork. If implementers agree to include it, the TIP editors will update the state of your TIP to 'Accepted'. 

- For all other TIPs, open a PR changing the state of your TIP to 'Final'. An editor will review your draft and ask if anyone objects to its being finalized. If the editor decides there is no rough consensus, they may close the PR and request you fix the issues in the draft before trying again.

****

## TIP Status

TIPs are separated into several statuses.

- **Draft**: A TIP that is undergoing rapid iteration and changes.  

- **Last Call**: A TIP that is done with its initial iteration and ready for review by a wide audience.  

- **Accepted**: A core TIP that has been in the Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author. The process for Core Devs to decide whether to encode a TIP into their clients as part of a hard fork is not part of the TIP process. If such a decision is made, the TIP will move to the final.  

- **Final (non-Core)**: A TIP that has been in the Last Call for at least 2 weeks and any technical changes that were requested have been addressed by the author.  

- **Final (Core)**: A TIP that the Core Devs have decided to implement and release in a future version or has already been released.

- **Active**: If the TIPs are never meant to be completed, the TIPs may have a status of “Active”. 

- **Abandoned**: If a TIP is no longer pursued by the original authors or it may not be a (technically) preferred option anymore.

- **Rejected**: A TIP that is fundamentally broken or a Core TIP that was rejected by the Core Devs and will not be implemented. 

- **Superseded**: A TIP which was previously Final but is no longer considered state-of-the-art. Another TIP will be in the Final status and cite the Superseded TIP.

- **Deferred**: A TIP which isn't accepted now, it may be accepted in the future. 

****

## TIP Types

TIPs are separated into several types, and each has its list of TIPs.

* **Standard Track**: Describes any change that affects most or all TRON implementations, such as a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using TRON. Furthermore, Standard TIPs can be broken down into the following categories. 

   **1.Core**: Improvements requiring a consensus fork, as well as changes that are not necessarily consensus critical but may be relevant to "core dev" discussions.    

  **2.Networking**: Includes improvements around network protocol.      

  **3.Interface**: Includes improvements around client API/RPC specifications and standards.    

  **4.TRC**: Application-level standards and conventions, including contract standards such as token standards (TRC-20).    

  **5.TVM**: Includes improvements around TRON Virtual Machine.    

* **Informational**: Describes a TRON design issue, or provides general guidelines or information to the TRON community, but does not propose a new feature.

For further discussion, please enter [Telegram](https://t.me/troncoredevscommunity)  
