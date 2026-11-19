---
tip: XXXX
title: "AVP-DS: Increasing the Number of Confirmed Transactions Through Address-Based Parallel Validation Paths and Separation of the Decision Layer from the Execution Layer"
author: Ali (@alichatme)
status: Draft
type: Standards Track
category: Core
created: 2026-07-11
discussions-to: https://github.com/tronprotocol/tips/issues/905
---
# AVP-DS
**Address-Based Validation Paths — Dynamic & Smart**

### Increasing the Number of Confirmed Transactions Through the Creation and Expansion of Address-Based Parallel Validation Paths and Separation of the Decision Layer from the Execution Layer
___
___
# Introduction

Blockchain networks, given the increase in the number of users, the growth of economic activities, and the expansion of their applications, always require higher processing capacity and a capability for sustainable growth so that they can increase the number of confirmed transactions in the network in proportion to the growth of incoming transactions.

However, increasing transaction processing capacity does not depend solely on hardware resources; factors such as how transactions are routed, workload distribution, the organization of parallel validation paths for transactions, and the utilization of new capacities also play an effective role in increasing transaction confirmation capacity and in using network capacity more effectively.

Improving scalability requires examining how transaction flows can be organized more effectively, without compromising the fundamental requirements of the protocol, the correctness of transaction processing, or the consistency of the network's final state.

Various solutions have been proposed to improve blockchain scalability, including parallel execution of independent transactions, increasing the capacity of each block, Layer 2 solutions (such as rollups and sidechains), and sharding (dividing state and processing load among independent shards). The effectiveness of each approach depends on the design of the network protocol, how transactions access shared state, and the degree of integration with the fundamental rules of the network (consensus, state transition, and ledger).

The AVP-DS capability, by separating the decision layer from the execution layer in a network and by organizing and creating address-based parallel validation paths, offers an effective approach to increasing the network's processing capacity. The goal of this capability is more efficient distribution of transactions based on the instructions and permits issued by the network protocol; in such a way that parallel validation paths are created and expanded not by default or pre-determined, but dynamically and based on addressing and the permit issued by the network protocol. These paths are considered in accordance with the current capacity of the network or new hardware and software capacities—such as new signature algorithms, new nodes, or new execution engines. This approach increases transaction confirmation capacity without replacing the fundamental mechanisms of the network—such as consensus, state transition, or the ledger structure.

### 1. Separation of the Decision Layer from the Execution Layer

One of the main principles of the AVP-DS capability is the separation of the decision-making layer regarding the permitted validation path of transactions from the components responsible for validation in the network. In this framework, the network protocol is the authority for issuing permits to route transactions to the network and to place them in the permitted validation path. The instructions regarding the processing path, the permitted components, and the validation conditions are determined within the same issued permit, and the network components act based on the instructions contained in the permit and within the scope of the components specified therein.

This separation is carried out with the aim of using parallel validation paths and providing a basis for organizing these paths according to the path specified in the permit and the rules of the network protocol. Path changes, handling invalid or dependent transactions, and management of exceptional conditions are carried out in accordance with the rules and mechanisms of the network protocol. After the permit is issued and the components and validation path are determined therein, no path or component outside the framework of the issued permit is valid, and all network components are required to comply with the instructions and the processing path specified in the permit.

### 2. Address-Based Parallel Validation Paths

The AVP-DS capability focuses on creating and expanding parallel validation paths using the mechanism of addressing transactions. Its goal is to provide a framework for routing transactions to parallel paths for validation, using the division of the network's existing hardware capacity and the effective distribution of incoming transactions among these groups.

In this approach, validation paths are not limited to a single fixed path; rather, the possibility of expanding them based on the number and type of incoming transactions and based on the permit issued by the network protocol for each transaction is considered and executed.

When issuing a permit, the network protocol, based on the received information, makes the necessary decisions regarding sequential validation or parallelization, as well as transactions requiring a specific order. Transactions requiring a specific order are managed for conflicts by the network protocol before entering the network, and are then sent for validation with the issuance of a permit and addressing to the components specified in the permit.

The role of AVP-DS in the network is solely to add a capability, not to impose a requirement or interfere with existing mechanisms. This capability only adds the possibility of creating and expanding address-based parallel validation paths to the network and does not create any requirement for its use; it also does not create any change in the consensus algorithm, ledger structure, state transition logic, or the native validation rules of the network. All decisions regarding sequential or parallel validation, path determination, conflict management, and permit issuance are made exclusively within the framework of the policies and rules of the network protocol, and AVP-DS has no interference in these mechanisms. In other words, AVP-DS is an optional and activatable platform that, if the network protocol decides, places the existing processing capacity and new capacities at the disposal of parallel validation paths.

### 3. Addressing Based on Existing and Added Capacity to the Network

One of the important goals of the AVP-DS capability is to provide parallel validation paths using addressing and determining the validation path in real time and in the form of a permit for each transaction by the network protocol.

This mechanism is not limited solely to the capacity existing at the time of launching the capability; rather, this capability provides the possibility of utilizing new capacities that are added to the network in the future, through organization into new parallel processing paths.

In this approach, the network protocol, using the addressing mechanism and based on usable capacity and the defined rules of the network, determines the minimum and maximum permitted validation paths for various types of transactions. When new processing capacities are added to the network, the network protocol, by addressing transactions and determining the validation path of each transaction from the moment of entry into the network until registration in the ledger in the form of permit issuance, uses the added capacity to confirm transactions.

In this way, the AVP-DS capability, with the aim of providing the possibility of gradual expansion of new parallel validation paths, increases the network's transaction confirmation capacity in proportion to the increase in the input of hardware capacity added to the network and the increase in parallel validation paths; in such a way that with the request for transactions to enter the network, new parallel validation paths are added and the volume of confirmed transactions in the network increases.

These transaction confirmation capacities include the use of the current and available hardware capacities of the network in the first stage and the capacities added in subsequent stages to the network.

In this framework, existing capacities and newly added capacities are used with organization for transaction confirmation and provide the basis for effective distribution of processing load based on addressing. The number of active paths is determined dynamically and in proportion to the increase in incoming new transactions to the network, based on the permit issued by the network protocol and in real time.

Adding parallel paths increases the input validation capacity to the network and consequently raises the number of confirmed and finalized transactions, without increasing the base TPS of the network or the TPS of the network's execution engine. This increase results from the distribution of incoming transactions among parallel validation paths and the effective use of existing capacity or capacity added in the future. The degree of utilization of the new capacity depends on factors such as the number of incoming transactions, the maximum permitted validation paths that can be created based on the network's existing hardware capacity, the conflict management capacity for sending incoming transactions to parallel validation paths, and the limitations existing under the network protocol.

The goal of this capability is to add parallel validation paths in proportion to the rate of incoming transaction requests to the network, so that the basis for effective use of existing capacity or capacity added in the future to the network is provided; this goal is realized based on addressing and separate determination of the validation path of each transaction in the network and based on the permit of the network protocol.

### 4. Preserving the Current Mechanisms of the Network

The AVP-DS capability, with the aim of improving and organizing validation paths and effectively using the current capacity of the network, is designed based on the important principle of separating the decision layer from the execution layer. This capability does not create any change in initial validation, transaction execution engines, state transition, consensus, block production, finalization, or registration of results in the network ledger.

The AVP-DS capability is presented with the aim of organizing and expanding parallel validation paths and within the framework of the native mechanisms of the network. Therefore, changes in validation paths, the manner of using new capacity, or the allocation of transactions are always carried out in line with the rules and under the supervision of the network protocol, and consequently do not undermine the correctness of processing or the requirements for transaction finalization.

In this approach, the network protocol is the authority for issuing the necessary permits and determining the instructions for routing transactions within the same permit for organizing parallel validation paths.
___
___
# Conflict Management in Parallel Execution with Network Support of the AVP-DS Capability

The continuous growth of the blockchain ecosystem, the increase in transaction volume, the expansion of active accounts, and the development of smart contracts and on-chain applications have transformed blockchain networks into one of the world's most important financial and digital infrastructures. The continuity of innovations and the expansion of this technology's applications further highlights the role of blockchain networks in shaping the future of the global financial system.

Current blockchain network architectures have demonstrated remarkable stability and performance; however, the growth in demand and the increase in operational volume — particularly in high-traffic networks — have placed increasing pressure on the validation and execution capacity for transactions.

The continuation of these mechanisms, without leveraging innovative solutions, will in the long term increase the gap between the network's operational capacity and the volume of incoming requests.

In contrast, the development and deployment of new architectures makes it possible to expand the validation and execution capacity for transactions in proportion to the network's demand.


The long-term evolution of networks — including support for parallel validation and execution of transactions, and increasing the number of confirmed transactions in proportion to the growth of incoming requests — requires a novel mechanism in the admission system, validation, and other network components.

This capability must enable the dynamic expansion of validation lanes, without requiring changes to the network's validation and consensus protocols.


Parallel validation, aimed at increasing confirmed transactions, and horizontal scaling of networks (adding parallel validation lanes) as opposed to vertical scaling (increasing the speed of each validation lane), have become one of the most important practical research directions in blockchain scalability.

Existing approaches in this field — including optimistic execution, dependency analysis, speculative execution, locking mechanisms, access-list-based scheduling, and object-oriented execution — attempt to enable parallel execution and increase the network's throughput by identifying, preventing, or managing transaction conflicts.

As the number of concurrently executed transactions increases, so does the likelihood of their simultaneous access to shared data and states. Therefore, conflict management is one of the determining factors in the productivity gained from parallelization. The higher the cost of identifying and resolving conflicts, the more of the capacity gained from adding parallel lanes will be consumed by managing these conflicts.

### Why Does Conflict Limit Horizontal Scaling?

The relationship between horizontal scaling and conflict management can be explained as follows:

1. Horizontal scaling means increasing parallel execution capacity by adding more validation lanes.
2. As the number of lanes increases, the possibility of executing more transactions concurrently is provided.
3. As concurrent transactions increase, so does the likelihood of multiple transactions accessing shared states and data.
4. In the event of a conflict, the network must, in order to preserve the correctness of the final state, respect the execution order of related transactions. Depending on the conflict management mechanism, this may lead to waiting, temporary suspension, rescheduling, re-execution, or rollback of part of the operations.
5. Therefore, if conflict management is not efficient, the cost of handling conflicts can eliminate a significant portion of the capacity gained from adding parallel lanes.

Hence, conflict management is one of the important bottlenecks in the effective exploitation of horizontal scaling.

With network support of the AVP-DS capability, this very bottleneck is targeted: by predicting conflicts before the transaction enters the network, determining the validation path, and managing the order of related transactions, the cost arising from conflict is reduced.

Today, the use of a fixed and pre-determined validation path in the network is no longer sufficient to respond to the volume and diversity of incoming requests, and leads to execution bottlenecks, increased queue lengths, unbalanced load distribution, and reduced network productivity.

Under such conditions, as incoming requests increase, the network is no longer able to validate all requests, because the validation capacity — due to the limited number of validation paths — remains limited.

The AVP-DS Solution

Level One — Prediction and Prevention of Conflict, Before the Transaction Enters the Network: The Network Protocol, upon receiving the transaction submission request from the wallet, reviews the network state and related transactions, and by issuing the Execution Permit, determines the validation path, responsible components, and appropriate conflict management policy for each transaction. At this stage, in addition to determining the path, the Network Protocol also specifies the order of handling related transactions, so as to prevent the concurrent execution of incompatible operations and, consequently, the creation of conflict.

Level Two — Conflict Management After the Transaction Enters the Network: If one of the execution components, during validation or execution, identifies a conflict or exceptional condition, it first verifies and reviews the Execution Permit and the completed stages, and then sends the relevant report to the Network Protocol and waits for a response. Decision-making regarding how to manage the conflict and continue the process rests exclusively with the Network Protocol, and none of the execution components are permitted to independently decide on how to handle the identified conflict.

In this manner, with network support of the AVP-DS capability, conflict management transforms from a purely reactive mechanism into a two-level process: prevention before the transaction enters the network, and controlled management of identified cases after its entry. The goal of this approach is to reduce the need for rollback and re-execution of transactions and to increase the productivity gained from horizontal scaling.


Hence, with network support of the AVP-DS capability, a fundamentally different and innovative approach is adopted for achieving network growth — in the direction of increasing transaction validation. The most important feature of this approach is the separation of the Decision Layer from the Execution Layer.


The parallelization approach, by leveraging the existing capacity and current components of the network — creates parallel validation lanes dynamically and based on the volume of incoming transactions — and acts in accordance with the priorities, rules, and required difficulty level for validation, on a per-transaction basis.

This approach moves the starting point of transaction management from the stage after the transaction enters the network to the stage of the transaction submission request in the wallet and before its final signing. At this stage, the wallet sends the information required for admission and initial assessment of the request to the Network Protocol, and the Network Protocol, after review, issues the Execution Permit appropriate to that transaction.

### Next Priority: Horizontal Scaling of the Network

Horizontal scaling of the network becomes possible through the dynamic formation of parallel validation lanes in proportion to the increase in incoming requests. The Network Protocol, using the existing hardware capacity and the capacities that will be added to the network in the future, dynamically determines the number and composition of required lanes.

This process is carried out based on conflict management, appropriate path selection, and designation of validation components on a per-transaction basis, so that the network's parallel capacity expands according to demand and available resources.

Difference from Conventional Networks

In many conventional architectures, parallel execution capacity depends on a pre-defined execution structure and resources, and changing the composition of execution paths usually requires architectural or configuration changes.

With network support of the AVP-DS capability, the network — in a different manner — forms validation lanes as dynamic software paths, using existing components or current capacity and under the management of the Network Protocol. The Execution Permit determines the path and components required for each transaction, and the Network Protocol, based on the volume of requests and available resources, provides the possibility of forming and allocating more lanes.

Whenever new hardware capacity is added to the network, the Network Protocol, using the addressing mechanism and the Execution Permit, organizes and employs that new capacity within validation paths.

Therefore, the number and composition of validation lanes, with network support of the AVP-DS capability, are not limited to a fixed and pre-determined structure, but can be expanded dynamically and in proportion to the network's resource capacity.

### The Central Role of the Execution Permit in Creating Parallel Validation Lanes

With network support of the AVP-DS capability, parallel validation lanes are formed as dynamic software paths on a per-transaction basis, not as fixed and pre-determined hardware paths.

The Execution Permit is the basis for creating, allocating, and organizing parallel validation lanes on a per-transaction basis. The Network Protocol, by reviewing the conditions, the number of incoming transaction requests, and the minimum validation difficulty level required under network rules, determines — through the issuance of the Execution Permit — the roadmap and dedicated validation path of each transaction.

This path includes the designation of initial validation nodes, the least-loaded execution engine from among the parallel execution engines of a domain, and other components required to complete the validation of a transaction — from the moment the transaction submission request is sent by the wallet to the Network Protocol until the monitoring of the expected outcome and the registration of the final validation result in the network ledger.

Accordingly, parallel validation lanes are formed and organized dynamically, not as public and fixed paths for the entire network, but in accordance with the issued Execution Permits and on a per-transaction basis.

The designation of the validation roadmap in the Execution Permit, on a per-transaction basis, means that the transaction — in accordance with the designated components — after passing through each validation stage, is directed along its dedicated path in the Execution Permit to the next designated execution component.

In this manner, the parallel validation lane for each transaction is formed through the selection and logical connection of the required network components within a specific execution path. These paths are formed using the existing hardware capacity and the capacities that will be added to the network in the future, in a software manner and under the management of the Network Protocol on a per-transaction basis, and are allocated through the issuance of the Execution Permit.

Therefore, the Execution Permit is not merely a routing instruction; it is the Network Protocol's primary mechanism for forming, designating, and dynamically allocating parallel validation lanes on a per-transaction basis in the network.


With network support of the AVP-DS capability, the Network Protocol is the authority for decision-making and lifecycle management of the transaction. The Network Protocol, upon receiving the transaction submission request from the wallet — containing the information required under the rules of the Network Protocol, before signing and before the transaction enters the network — and upon receiving the required information from the network (including real-time load monitoring, the number of transactions under validation, and other required information), makes the decisions regarding admission of the request, validation path, selection of relevant components, execution domain, the least-loaded execution engine from the designated domain, and conflict management policy, and records them in the Execution Permit.

After receiving the Execution Permit, the wallet grants the user permission to sign the transaction, and then sends the transaction — along with the Execution Permit and the per-permit encryption key — to the initial validation nodes designated in the Execution Permit.

The transaction, in accordance with the stages and components designated in the Execution Permit, after passing through each validation stage, is directed along its dedicated path to the next designated execution component.

The members designated in each Execution Permit are not permitted, at any stage of validation, to make independent decisions; all stages must be performed exactly in accordance with the issued Execution Permit.

### With network support of the AVP-DS capability, the Network Protocol assumes the following responsibilities:

- Receiving the transaction submission request, including the information required to review the request, from the wallet, in accordance with the rules of the Network Protocol
- Analyzing the received information, including the sender's address, the receiver's address, the asset type, the access list, and other metadata required for issuing the Execution Permit
- Applying admission policies and checking Sender Consistency, using network state information and analytical reports of previous conflicts
- Reviewing transactions under validation and related transactions, in order to determine the order of handling them and to prevent the concurrent execution of incompatible operations
- Dynamically selecting validation nodes for each transaction, based on network policies and the minimum permitted difficulty level under protocol rules
- Dynamically forming the validation lane of each transaction, through the selection and designation of a path among validation nodes, execution domain, execution engine, and other required components — up to the monitoring of behavior and expected outcome and the registration of the final result in the ledger
- Designating the execution domain and classifying transactions, including TRX, USDT, NFT, and other operation types
- Selecting the least-loaded execution engine of a domain, based on monitoring the load of execution engines at the time of issuing the Execution Permit
- Designating the conflict management policy on a per-transaction basis, at two levels: prevention before the signed transaction enters the network, and management of conflict or exceptional condition after the signed transaction enters the network
- Issuing the Execution Permit, including the information required for validation, the designated path and components, addressing, routing, transaction direction, conflict management policy, and other instructions necessary to complete the transaction lifecycle
- Encrypting the Execution Permit with a per-permit encryption key, storing the encrypted copy in the Provisional State under the control and supervision of the Network Protocol, and sending a copy of the Execution Permit along with the corresponding per-permit encryption key to the requesting wallet, in order to provide the possibility of verification in the network

The responsibility of the Network Protocol begins upon receiving the transaction submission request from the wallet and continues until the final status of the transaction is determined — that is, the review of the behavior or final outcome and the registration of the transaction in the network ledger.

With network support of the AVP-DS capability, the Network Protocol is responsible for all decisions regarding the designation of the validation roadmap, addressing, dynamic selection of nodes, domain selection, selection of the least-loaded engine from among the parallel engines of a domain, and management of exceptions and conflicts if identified — throughout the entire transaction lifecycle.

### One of the Fundamental Innovations of the AVP-DS Capability: Execution Permit–Based Conflict Management at Two Levels

- Level One: Prediction and prevention of conflict, before the signed transaction enters the network.
- Level Two: Identification and management of conflicts and exceptional conditions, after the transaction enters the network.

In many conventional architectures, a significant portion of conflict management is performed after parallel execution has begun and dependencies or actual collisions have been identified. This process may require rescheduling, building a dependency graph, waiting, re-execution, or the use of locking mechanisms.

With network support of the AVP-DS capability, a different approach is adopted: transaction management begins from the stage of the transaction submission request in the wallet. At this stage, before the final signing of the transaction, the transaction submission request, including the required information, is sent to the Network Protocol so that the protocol can review the received request and, after receiving the required information from network components, make the decisions regarding admission, validation path, addressing, routing, execution domain, execution engine, and conflict management policy.

All decisions related to validation — on a per-transaction basis, including the designation of the roadmap, the designation of relevant components, routing, and addressing — from the moment of the transaction submission request and before the transaction is sent to the network, up to the monitoring of the expected outcome and the registration of the final result in the network ledger, are recorded in the Execution Permit and, along with the transaction, are communicated to the relevant components — and not to the entire validation capacity of the network.

As a result, this innovation moves conflict management from the stage after the transaction enters the network (in conventional networks) to before the transaction enters the network — and to the moment of the transaction submission request in the wallet.

### Conflict Management

With network support of the AVP-DS capability, conflict management is part of the Network Protocol's decision-making process and is performed in two stages:

- Prediction and prevention of potential conflicts, at the time of issuing the Execution Permit and before the transaction enters the network
- Identification of conflicts or exceptional conditions by the execution components designated in the Execution Permit, after the transaction enters the network

Stage One — Prediction and Prevention of Conflict, Before the Transaction Enters the Network

With network support of AVP-DS, the Network Protocol, before issuing the Execution Permit and before the signed transaction enters the network, reviews the information of the submission request sent from the wallet against the real-time network state, the transactions under validation, and the analytical information from previous conflicts.

Based on this review, the Network Protocol assesses the likelihood of dependency or conflict among transactions and takes appropriate preventive measures. These measures may include designating a compatible validation path, selecting responsible components, determining the order of handling related transactions, and recording the appropriate conflict management policy in the Execution Permit.

In this manner, the Network Protocol, for each transaction, before its entry into the validation and execution process, designates the roadmap and the necessary instructions. This process, using the request information, the network state, and the experience gained from previous conflicts, provides the possibility of reducing the likelihood of recurrence of similar conflicts.

Stage Two — Conflict Management After the Transaction Enters the Network

At this level, whenever one of the execution components related to the validation and execution of the transaction — for example, the execution engine — identifies a conflict or exceptional condition during validation, the following actions are taken:

- Verification of the Execution Permit and review of the validation stages. The component that has identified the conflict must, as its first action, verify the transaction's Execution Permit and review the completed validation stages. This review is carried out with the aim of ensuring the validity of the Execution Permit, the conformity of the transaction with the path designated by the Network Protocol, and the correctness of the performance of the previously designated components. In this manner, it is determined whether the validation stages have been correctly performed in accordance with the instructions of the Execution Permit and in accordance with the roadmap designated by the Network Protocol.
- Reporting to the Network Protocol and waiting to receive a decision. After completing the review, the component identifying the conflict prepares a report containing the conflict information, the result of the Execution Permit verification, and the results of the review of the validation stages, and sends it to the Network Protocol. Regardless of the outcome of the review, the relevant component must send the report to the Network Protocol and wait until it receives a response and instructions.

Decision-making regarding how to manage the conflict and continue the process rests exclusively with the Network Protocol. None of the execution components are permitted to independently, and outside the instructions of the Network Protocol, change the validation path or the manner of handling the conflict.

The Network Protocol, based on the received report and the current state of the transaction, issues the necessary instructions for continuing the process. These instructions may include actions such as the following:

- Continuing validation or execution from the specified stage
- Re-executing the transaction in the execution engine that identified the conflict
- Issuing a new Execution Permit and resending the transaction to new validation components, if a change of path, addressing, or composition of execution components is needed
- Or any other action that the Network Protocol deems necessary under its rules and policies

All network components are required to act in accordance with the received response and the instructions issued by the Network Protocol.

Prevention of Recurrence of Identified Conflicts. The Network Protocol, for each identified conflict or exceptional condition, prepares an analytical report containing the manner of identification, the cause, the handling method, and the final outcome, and uses these reports to improve the policies for transaction admission, scheduling, selection of validation nodes, selection of the execution domain, selection of the execution engine, and other policies related to the issuance of the Execution Permit — for the purpose of analyzing and preventing the recurrence of conflict.

In this manner, the information obtained from past conflicts is used in the subsequent decision-making of the Network Protocol, so that the recurrence of similar conflicts in the validation of future transactions — from the request stage — is predicted and prevented.

### Foundations of the Effectiveness of Conflict Management in the AVP-DS Capability

Three Fundamental Pillars

With network support of the AVP-DS capability, conflict management rests on three fundamental pillars; each of these three pillars plays a determining role in its effectiveness and correctness:

- Separation of the Decision Layer from the Execution Layer
- Transfer of transaction management from after entry into the network to before its entry — in the wallet and before signing
- Addition of addressing and designation of the validation path of transactions with support of the AVP-DS capability

Why Do These Three Pillars Make Conflict Management Possible?

The answer lies in a fundamental point: conflict management in conventional architectures is performed after the occurrence of conflict, with reactive mechanisms — whereas these three pillars transfer conflict management to the stage before its occurrence.

- Separation of the Decision Layer from the Execution Layer enables the Network Protocol, before any execution decision, to designate the path and responsible components.
- Transfer of transaction management to before entry into the network enables the Network Protocol, before the signing of the transaction and before its submission, to be aware of the existence of related or under-confirmation transactions.
- Addressing and designation of the validation path enables the Network Protocol, for related transactions, to designate identical or compatible paths and to prevent the collision of paths.

The result of combining these three pillars is the provision of the possibility of proactive conflict management and the reduction of the cost of handling conflicts at execution time. This can increase the productivity gained from adding parallel validation lanes and provide the ground for horizontal scaling of the network.

Two Assumptions with the Highest Conflict Rate

To demonstrate the effectiveness of these three pillars, two assumptions of conflict management that produce the highest conflict rate are examined:

Example 1 — Related Transactions from One Account or to One Account

Suppose account A has a transaction under execution in the network. At the same time:

- Account A sends another transaction submission request to the Network Protocol; or
- Account B presents a transaction submission request that is related to account A.

Under these conditions, the Network Protocol, being aware of the existence of a transaction under confirmation related to account A, when issuing the Execution Permit for the new requests, designates a shared and coordinated path with the path of the transaction under execution. This path includes the initial validation nodes, the domain, and the parallel execution engine designated.

Therefore, the Execution Permits issued for these related transactions designate identical validation and execution components, and their roadmap — from the stage of receiving the transaction submission request to the registration of information in the network ledger — will be shared.

As a result, the related transactions, instead of being distributed among independent parallel lanes and execution engines, are executed in a shared and coordinated path. This approach prevents the creation of independent execution paths for transactions that are related to one another and provides the possibility of coordinated management of them.

With network support of the AVP-DS capability, the possibility of using parallel validation paths for independent transactions is preserved; while the Network Protocol, for related transactions, designates a shared and coordinated path. In this manner, parallelization for independent transactions and shared routing for related transactions become possible alongside each other.

The Network Protocol, as long as there are transaction submission requests related to account A or transactions under execution related to it, maintains the shared path for new related requests. After the completion of the execution of previous transactions and the absence of a related request or transaction under execution, the Network Protocol can, for subsequent requests, designate a new validation and execution path in accordance with the real-time conditions of the network.

Example 2 — High-Traffic Accounts (such as Exchanges)

Suppose the account of an exchange continuously receives from various accounts and sends to various accounts, and a large number of transaction submission requests to the destination of this account or from its origin are presented to the Network Protocol.

Under these conditions, the Network Protocol, using the information received before the signing of the transaction and its submission from the wallet, identifies the requests related to the exchange account. Then, when issuing the Execution Permit, for transactions that are related to each other's state or operations, it designates a shared and coordinated path including the initial validation nodes, the domain, and the parallel execution engine.

In this manner, the Execution Permits issued for the related transactions designate identical validation and execution components, and their roadmap — from the stage of receiving the transaction submission request to the registration of information in the network ledger — will be shared. This approach provides the possibility of coordinated management of transactions related to the exchange account and prevents the creation of independent execution paths for operations dependent on one another.

In contrast, transactions that, from the perspective of account states and execution operations, do not have effective dependency or relationship with one another, can be directed through independent Execution Permits to different parallel lanes, validation nodes, domains, and execution engines. Therefore, the high-traffic nature of an account by itself does not cause all transactions related to it to be confined to a single path; rather, the type of relationship and dependency of transactions will be the basis of the Network Protocol's decision for choosing a shared or parallel path.

The Network Protocol can also, considering the information received before the signing of the transaction, the real-time network state, execution records, and information obtainable from smart contracts, predict potential conflicts and, at the time of issuing the Execution Permit, designate the appropriate path for preventing and managing them.

Three Principles Governing This Approach

The examples presented demonstrate the Network Protocol's capability in predicting, preventing, and managing conflicts based on three fundamental principles:

1. Separation of the Decision Layer from the Execution Layer: The Network Protocol is the decision-making authority and is responsible for designating the path, selecting validation and execution components, and managing conflicts; while the execution components perform the designated tasks in accordance with the Execution Permit.
2. Managed Admission, instead of Unmanaged Admission: Transaction submission requests, before the signing and entry of the transaction into the network, are reviewed by the Network Protocol so that execution conditions, potential dependencies, and predictable conflicts are identified.
3. Dedicated Routing, Addressing, and Direction of Transactions: The Network Protocol, using the Execution Permit, designates the path and required components of each transaction on a dedicated basis. Accordingly, independent transactions can use parallel validation paths and different execution engines; while for related transactions, a shared and coordinated path is designated so that the possibility of coordinated execution and management of them is provided.

All of these processes are carried out under the supervision of the Network Protocol and through the Execution Permit mechanism, and none of the execution components independently have the authority to change the decisions and the designated path.

Conclusion

The prediction of conflicts from the stage of receiving the transaction submission request, alongside dedicated routing for independent transactions and shared and coordinated routing for related transactions, enables the Network Protocol to effectively reduce the conflict rate and manage it at a low level.

The reduction of the conflict rate prevents the waste of resources caused by unsuccessful and repeated executions and increases the network's capacity to confirm a larger number of independent transactions — through parallel paths.

As a result, with network support of the AVP-DS capability, the ground for continuous horizontal scaling and extensive scalability of the network is provided.

### The Execution Permit: The Validation Roadmap of Each Transaction

The most important innovation of AVP-DS is the separation of the Decision Layer from the Execution Layer and the use of the Execution Permit to designate and manage the validation path on a per-transaction basis.

With network support of the AVP-DS capability, the Network Protocol, instead of unmanaged admission of transactions, uses the Managed Admission mechanism. In this mechanism, before the signed transaction enters the network, the initial request is reviewed, and the Network Protocol, by issuing the Execution Permit, designates the validation path, addressing, routing, transaction direction, and responsible components.

These three fundamental principles — namely the separation of the Decision Layer from the Execution Layer, Managed Admission, and the dynamic formation of the validation path using the Execution Permit — provide the ground for predicting and managing conflicts and for more effective exploitation of parallel lanes.

All stages of the validation of a transaction — from the transaction submission request in the wallet to the monitoring of the expected outcome and the registration of the transaction in the ledger — are designated by the Network Protocol and recorded in the Execution Permit. This permit acts as the reference validation contract for the entire transaction lifecycle — from the moment of the transaction submission request by the wallet to the monitoring of the expected outcome and the registration of the validation result in the network ledger.


The Execution Permit is a software contract and the reference for the validation instructions of each transaction, issued by the Network Protocol. This permit includes the validation roadmap, addressing, routing, and direction of the transaction to the designated components of the network.

The Network Protocol, using the Execution Permit, forms the validation lane of each transaction dynamically and in a software manner. This lane is formed through the selection and designation of the combination of required network components, including initial validation nodes, execution domain, execution engine, and other relevant components.

The number and composition of validation lanes are determined based on the volume of incoming requests, the validation requirements, the policies of the Network Protocol, and the available execution resources. These resources may include the existing hardware capacity of the network and the capacities that will be added to the network in the future.

In this manner, the Network Protocol can, in proportion to demand and available resources, dynamically form parallel validation lanes and communicate the Execution Permit corresponding to each transaction to the designated components, along with the transaction.

The Execution Permit includes the following information and instructions:

- The identifier of the Execution Permit and its validity period
- The permitted signature algorithm
- The initial validation nodes selected
- The validation path and roadmap, including addressing, routing, and direction of the transaction to the relevant components
- The designated execution domain
- The least-loaded execution engine from among the parallel engines of a domain
- The order of handling or the necessary instructions for coordination with related transactions, if needed
- The conflict management policy and the instructions for handling exceptional conditions
- Other parameters and protocol information required to complete the validation process and the final registration of the transaction

After the issuance of the Execution Permit:

1. The wallet, based on the permit, sends the signed transaction, along with the Execution Permit and the per-permit encryption key, to the related initial validation nodes designated.
2. The initial validation nodes, as their first action, use the per-permit encryption key received from the wallet to decrypt the encrypted copy of the Execution Permit retained in the Provisional State, and then verify the permit received from the wallet against the decrypted copy, line by line. After completing the initial validation, they direct and send the transaction, together with the Execution Permit and the per-permit encryption key — without any new decision-making and solely based on the information in the Execution Permit — to the designated execution domain and execution engine.
3. The execution engine executes the transaction in accordance with the designated path and sends it to the next designated components.
4. All stages are performed in accordance with the roadmap designated in the Execution Permit, on a per-transaction basis and according to its designated components; and none of the components are permitted to make a decision or take an action independently and outside the instructions of the Execution Permit.
5. After monitoring and comparing the expected outcome or behavior with the result obtained from the validation, the transaction is registered in the network ledger.
6. In the event of an exception or conflict, the identifying component first re-verifies and reviews the Execution Permit and the completed stages, then sends a report to the Network Protocol and waits to receive a response.

All validation and routing stages of the transaction, from the moment of the issuance of the Execution Permit to the finalization of its status, are pre-determined in the Execution Permit, and all network components are required to act accordingly. All validation stages must be performed in accordance with the Execution Permit issued by the Network Protocol.

### The Fundamental Achievements of AVP-DS

With network support of the AVP-DS capability, three fundamental new capabilities are added to the network:

- Separation of the Decision Layer from the Execution Layer
- Replacement of Managed Admission in place of Unmanaged Admission
- Dynamic formation of validation lanes and designation of the roadmap, addressing, routing, and direction of each transaction based on the Execution Permit

These three capabilities are employed under the management of the Network Protocol and through the Execution Permit issuance mechanism, with the aim of reducing conflicts, increasing the productivity of parallel execution, and providing the possibility of horizontal scaling of the network.

As a result, the network can, using the existing execution capacities and the capacities added in the future, validate and confirm a larger number of incoming transactions in proportion to its resources and operational conditions.

In the event of new hardware capacities being added, the Network Protocol, through the addressing and routing mechanism, employs the new capacities for transaction validation. In this manner, the network's execution capacity can increase in proportion to the increase in incoming transaction requests.

### Conflict Management in Smart Contracts and Internal Calls

With network support of the AVP-DS capability, to request interaction with a smart contract, the user sends a transaction submission request from the wallet to the Network Protocol.

Upon receiving this request, to prevent conflicts, the Network Protocol collects the necessary data from the network, including the contract's recorded content (such as its code and state) and previous execution records.

If the Network Protocol determines based on this data that the transaction might internally call other contracts during execution, upon issuing the Execution Permit, it considers the entire possible internal call chain as part of the same transaction and, accordingly, issues the Execution Permit along with the per-permit encryption key.

All network components complete the validation stages of the main contract and the potentially invoked internal contracts based on the roadmap and path specified in the permit. Therefore, potential internal calls do not receive separate permits and do not follow separate paths; because their independent execution along different paths could lead to conflict in the shared state.

If the Network Protocol receives other transaction submission requests related to the same contracts or shared state, being aware of the transaction under confirmation, it determines a shared path coordinated with the path of the transaction being executed when issuing Execution Permits for the new requests, and then issues the new permit.

If, during the execution of the smart contract and within the internal contract call, changing the path for the invoked internal contract becomes unavoidable, this event is considered an exceptional condition. In this case, the component identifying the exception first re-verifies the Execution Permit and, after reviewing the validation stages, sends the report to the Network Protocol and waits for a decision. In this state, the Network Protocol can issue a new Execution Permit including the new validation path.

All network components are required to act in accordance with the response and instructions issued by the Network Protocol. No network component is permitted to make independent decisions or take actions outside the Network Protocol's instructions within the framework of the Execution Permit.

### Parallel Validation with Sequential Execution Simulation

Preserving transaction order is one of the pillars of security and correctness in blockchain networks. Respecting validation order helps maintain the integrity of account states, prevent conflicts, prevent double-spending, ensure predictability of network behavior, and enable accurate auditing.

As networks move toward parallel validation, preserving the logical order among dependent requests becomes even more important; because the simultaneous execution of related requests leads to conflicts and state inconsistency in the network, and increases validation cost.

The AVP-DS capability manages this issue by enforcing order through a shared path at the Admission Layer and using the Execution Permit mechanism.

As a result, transactions related to each account are executed along a single path and sequentially — similar to the behavior of a network with sequential execution, but at the level of that account.

Other transactions from other accounts are organized by the Network Protocol, using the Execution Permit, across other parallel software execution paths — in line with transaction validation and utilizing the full hardware capacity of the network.


1. Enforcing Order through a Shared Path at the Admission Layer

With network support of the AVP-DS capability, the order of requests is enforced not by suspending permit issuance until the validation of the transactions under validation related to an account is complete — including sends and receives, smart contract invocations, and interactions with a shared state (whether a shared contract such as a decentralized exchange, or a shared account such as a centralized exchange) — but through the designation of a shared path for the new transaction with the transactions under validation, by means of the Execution Permit and based on the information received from the wallets in the form of transaction submission requests to the network.

When an admission request is received from a source account, the Network Protocol reviews the execution state of previous requests and the received requests related to that same account. Accordingly, it issues the Execution Permit for the new request with the same roadmap, path, and components designated for the previous request under validation, or for the received requests related to that same account.

Therefore, the execution order of requests is preserved through the shared path, not by suspending permit issuance until the validation of the transactions under validation is complete.

As a result, an account cannot bypass the execution order of its previous requests by submitting a new request, changing the fee amount, or choosing a different path — because the path remains the same. This rule applies equally to individual transactions and Bundles.


2. Independence from Submission Type

The sequential relationship between requests from the same account is independent of their submission type:

- A new individual transaction cannot bypass the execution order of a previous request from the same account by choosing a different path.
- A new Bundle cannot bypass the execution order of a previous request from the same account by choosing a different path.
- The number of transactions within a Bundle or the fee amount alone does not grant it priority over a previous request from the same account.

Therefore, the execution order of requests is determined by their logical and temporal relationship at the account level, not by the apparent form of submission or the fee amount.


3. Defense Against Reordering and Front-Running

This mechanism creates a new defensive layer against attempts to reorder transactions. If an attacker attempts to enter their transaction into the network earlier than the target transaction, they cannot deliver it to the network through a different validation path; because the permits issued for transactions related to a shared state — such as the same liquidity pool in a shared contract (for example, a decentralized exchange) or the balance of a shared account (for example, a centralized exchange) — with network support of the AVP-DS capability, must all follow the same path and components as the previous transactions under validation, through the Execution Permit mechanism for addressing, routing, and direction.

Therefore, submission time or submission path cannot bypass the defined order — because the path remains identical.


4. Benefits of Preserving Order in AVP-DS

· Preserving State Integrity: Respecting the order of requests prevents inconsistent states and certain double-spend scenarios.
· Reduced Race Conditions and Reordering: Consecutive requests from the same account cannot enter the execution path without respecting the required order.
· Predictability: Network behavior becomes clearer and more predictable for users and applications.
· Easier Auditing: The sequential relationship of requests and their results can be reconstructed and verified.
· Safe Parallelization: By preserving the order of requests within each account, requests from independent accounts — in terms of state — can be validated and executed in parallel; while requests related to a shared state (such as a shared contract or a shared account) are directed in a coordinated manner, in accordance with the shared-path policy.


5. Relationship with Conflict Management

Sequential validation does not replace conflict management; it is complementary to it.

Sequential validation at the level of each account is carried out by simulating the behavior of sequential validation in conventional networks within a single validation lane. This approach prevents a significant portion of conflicts — including conflicts caused by the improper order of requests from an account — at the Admission Layer itself and before entering execution.


6. Simulating Sequential Validation for Each Account

The path designated for the transactions of each account, in terms of the order of handling, functions similarly to the sequential validation approach in conventional networks; with the difference that, with network support of the AVP-DS capability, this order is confined to the specific path of that same account, and independent accounts can be handled simultaneously in other parallel execution paths. Within this framework, transactions that access a shared state — such as the same liquidity pool in a shared contract or the balance of a shared account — are directed according to the shared-path policy, so that the order and coordination of related transactions are also preserved.


7. Foundational Principle

Execution Permit issuance must respect, for requests related to a shared state — such as the same liquidity pool in a shared contract or the balance of a shared account — the same roadmap, path, and components designated for the previous request related to that same shared state. A subsequent transaction or Bundle must become eligible for admission with the same path and components as its related predecessor request — not with a new path.

This principle ensures that the order of requests related to a shared state cannot be bypassed by creating a new request, changing the fee amount, changing the submission path, or reconstructing a previous transaction; while preserving the network's parallelization capacity for requests from independent accounts.

In this manner, with network support of the AVP-DS capability, order is preserved at the level of each account and each shared state, while parallelization expands at the network level. These two — order and parallelization — are not in opposition, but in mutual evolution: each account follows its own sequential path; independent accounts advance simultaneously along parallel paths. This is the very balance between security and scalability that AVP-DS realizes at the network level.
___
___
# Economic Impact and Incentive Model

### 1. The Challenge of Traditional Architectures

In many blockchain networks, increasing the number of nodes beyond a certain threshold does not necessarily lead to an increase in the network's processing capacity. In these architectures, although more validators join the network, the transaction processing path remains limited by the fixed capacity of the network's validation and execution system.

Under such conditions:

- Revenue from fees is distributed among a larger number of nodes.
- The network's operational capacity remains approximately constant.
- The economic return of each node gradually decreases.
- Increased demand typically leads to longer queues and higher fees, rather than an increase in actual processing capacity.

For this reason, in many networks, the growth in the number of validators does not necessarily result in a proportional growth in network capacity.

### 2. ATHENA's Different Approach

ATHENA examines this issue from a fundamentally different perspective.

In the ATHENA architecture, increasing the number of nodes is not merely about adding more validators—it creates new capacity for expanding parallel validation and increasing the network's operational throughput.

Through unified transaction lifecycle management, ATHENA:

- Receives the required information from the wallet and the network.
- Dynamically selects the initial validator nodes, resulting in the creation of parallel validation pipelines in the network.
- Determines the appropriate execution domain.
- Selects the least-loaded execution engine among those operating in parallel within that domain.
- Issues the Execution Permit.
- Manages the validation path according to Host Protocol policies until the transaction is finally recorded in the global ledger.

Therefore, the addition of new nodes can directly increase the transaction admission and initial validation capacity. Subsequently, the Host Protocol, in response to increased load, can increase the number of execution engines in each domain.

As a result, validation capacity and execution capacity grow in a coordinated manner.

### 3. Positive Economic Feedback Loop

The ATHENA architecture enables the creation of a positive economic feedback loop.

This loop operates as follows:

1. New nodes join the network.
2. ATHENA organizes them into parallel validation pipelines.
3. Admission and initial validation capacity increases.
4. In response to increased load, the Host Protocol activates more execution engines across different domains.
5. More transactions enter the validation and execution cycle.
6. The number of transactions recorded in the global ledger increases.
7. Total network revenue increases.
8. Increased revenue creates greater incentive for new nodes to join.
9. The cycle repeats.

The stability of this cycle depends on the existence of real demand for incoming transactions and appropriate Host Protocol policies for developing the network's execution resources.

### 4. Conceptual Example

Assume a network has:

10,000 validator nodes with an approximate capacity of 1,000 transactions per second (TPS).

Now assume the number of nodes increases to 20,000.

In conventional architectures:

- The number of validators increases.
- Processing capacity remains approximately constant.
- Revenue is divided among a larger number of nodes.
- The economic return of each node decreases.

In the ATHENA architecture:

Assume the Host Protocol allows ATHENA, in the event of high incoming transaction demand, to form initial validation pipelines consisting of 200 nodes each, and distribute incoming transactions among these processing pipelines.

In this case, approximately 100 parallel validation pipelines could be formed, which could theoretically increase transaction validation capacity up to 100 times.

This example is provided solely to demonstrate the potential of the architecture and should not be interpreted as a guarantee of actual performance.

ATHENA distributes independent transactions among these parallel initial validation pipelines and, after initial validation, directs each transaction according to the Execution Permit to the relevant execution domain and the least-loaded engine within that domain.

If the network infrastructure, hardware resources, execution engines, and transaction demand all support this level of processing, the network's operational capacity could increase significantly.

### 5. Economic Impact

In ATHENA, revenue is not merely a function of the number of nodes—it is a function of the network's actual transaction processing capacity.

The more transactions the network can process using parallel validation and parallel execution engines:

- Total network revenue increases.
- Distributable revenue among participating validators increases.
- Economic incentive for investing in network infrastructure and joining new nodes increases.
- Gradual network expansion becomes possible without changing the base architecture.

Therefore, ATHENA transforms the increase in the number of nodes from a potential operational cost into an opportunity for operational capacity growth and economic network development.

### 6. Scope of This Analysis

The analysis presented in this section is conceptual and architectural in nature.

The actual performance of ATHENA will depend on multiple factors, including:

- Real transaction demand
- Host Protocol policies
- Node hardware capacity
- Execution capacity and the number of parallel engines in each domain
- Network bandwidth
- Implementation quality
- Consensus algorithm overhead
- Network economic policies
- Reward distribution mechanisms

Therefore, ATHENA does not guarantee a specific increase in TPS or validator revenue.

Rather, it provides an architectural framework that, under favorable conditions, can utilize existing network resources more effectively and facilitate the simultaneous growth of:

- Transaction admission capacity
- Parallel validation
- Parallel execution
- Economic efficiency
- Attraction of new nodes
- Development of execution engines
- Overall network operational throughput

All of this is achieved without changing the consensus algorithm, account model, or the unified global ledger.
___
___
# Comparison of ATHENA with Other Scalability Solutions

Improving scalability has long been one of the primary research objectives in blockchain technology, and numerous architectural approaches have been proposed to achieve this goal. Most existing solutions increase transaction throughput by modifying one or more fundamental components of blockchain architecture, such as the consensus algorithm, ledger organization, execution model, or transaction processing flow.

ATHENA pursues the same objective through a fundamentally different architectural philosophy.

Rather than redesigning the consensus protocol, partitioning the global ledger, modifying the account model, or replacing the native validation mechanism, ATHENA introduces an integrated transaction lifecycle management architecture that intelligently manages transactions from their admission into the network until their final commitment to the global ledger.

Within ATHENA, a transaction begins with an Admission Request submitted by the wallet according to the Host Protocol. ATHENA then collects the required contextual information from both the wallet and the network, dynamically selects the initial validator nodes, forms the initial parallel validation group, determines the appropriate execution domain, selects the least-loaded parallel execution engine within that domain, and generates an Execution Permit that defines the complete validation path of the transaction.

The Execution Permit becomes the authoritative validation contract for the entire transaction lifecycle. One copy is securely stored within the Canonical Copy for future verification, while another copy is delivered to the wallet, allowing the signed transaction to be forwarded to the designated validator nodes.

From this point forward, every component of the network—including validators, execution engines, consensus participants, and other protocol components—processes the transaction exclusively according to the information contained in the Execution Permit and the policies defined by the Host Protocol, without independently redefining the transaction's execution path.

Furthermore, ATHENA introduces a novel Execution Permit–based conflict management mechanism. Whenever execution conflicts or exceptional conditions are detected, ATHENA first re-verifies the Execution Permit and the completed validation path before managing the continuation of transaction processing according to Host Protocol policies. The transaction is therefore managed from the exact stage where the conflict is detected rather than restarting the entire validation lifecycle.

In addition, ATHENA generates analytical reports describing detected conflicts, their causes, applied resolution strategies, and final outcomes. These reports are provided to the Host Protocol as architectural feedback, enabling continuous improvement of future admission policies, scheduling decisions, validator selection strategies, execution domain assignment, execution engine selection, and Execution Permit generation.

Consequently, ATHENA improves the operational capacity of the network through intelligent lifecycle management, dynamic validator selection, parallel initial validation, intelligent execution scheduling, and proactive conflict management while remaining fully compatible with the native blockchain architecture.

### Comparison with Sharding

Sharding increases network throughput by partitioning the global state and ledger into multiple independent shards. Each shard maintains its own subset of validators and network state, requiring additional coordination mechanisms for cross-shard transactions.

ATHENA follows a fundamentally different approach.

It never partitions the network state or the global ledger. All validators continue operating on the same global state and unified ledger.

Instead of dividing the blockchain itself, ATHENA dynamically organizes validator nodes into parallel initial validation groups while maintaining a unified consensus process and a single global ledger.

### Comparison with Layer 2 Solutions

Layer 2 solutions typically improve scalability by moving a substantial portion of transaction execution outside the main blockchain and recording only the final settlement on Layer 1.

ATHENA adopts a different architectural model.

Transactions remain fully governed by the native protocol of the host blockchain. ATHENA intelligently manages transaction admission, initial validation, scheduling, execution domain selection, execution engine selection, and transaction lifecycle management without moving transaction ownership or validation outside the main protocol.

When supported by the Host Protocol, ATHENA may also direct transactions toward Layer 2 execution environments in addition to Layer 1 execution engines.

Therefore, ATHENA is neither a replacement for Layer 2 solutions nor an alternative to them. Instead, it functions as a complementary architectural layer capable of providing intelligent admission management and transaction scheduling alongside Layer 2 technologies.

### Comparison with Block Size Scaling

Some blockchain networks increase throughput by enlarging block size, allowing more transactions to be included in each block. Although this approach may improve throughput, it generally increases hardware requirements, bandwidth consumption, block propagation time, and node synchronization overhead.

ATHENA does not modify block size.

However, it remains fully compatible with any future block size adjustments introduced by the Host Protocol and can simultaneously benefit from larger blocks while continuing to optimize transaction admission, validation, and execution scheduling.

### Comparison with Consensus Algorithm Optimization

Some scalability approaches seek higher throughput by replacing or fundamentally modifying the consensus algorithm.

ATHENA intentionally avoids this approach.

Validation, voting, block production, and transaction finalization continue to operate entirely according to the native consensus mechanism of the Host Protocol.

Because ATHENA operates independently of the consensus algorithm itself, future modifications or upgrades to the consensus protocol can be adopted without requiring redesign or architectural changes within ATHENA.

### ATHENA's Architectural Position

From an architectural perspective, ATHENA can be viewed as an **Integrated Transaction Lifecycle Management Layer** operating within Layer 1.

Unlike other scalability approaches:

- Sharding increases capacity by partitioning network state and ledger.
- Layer 2  increases capacity by moving execution outside the main chain.
- Block size scaling increases capacity by enlarging individual blocks.
- Consensus optimization increases capacity by modifying the consensus mechanism.

ATHENA increases the network's operational capacity through intelligent lifecycle management, dynamic validator selection, parallel initial validation, execution domain classification, intelligent execution engine selection, Execution Permit–based validation management, and proactive conflict resolution, while leaving all fundamental components of the blockchain architecture unchanged.

For this reason, ATHENA is designed as a complementary Layer 1 architecture that can coexist with future scalability technologies, provided they remain compatible with the policies and operational constraints defined by the Host Protocol.
___
___
# Key Features and Mechanisms of the Network After Support of the AVP-DS Capability

### « Provisional State »

The Concept of Provisional State in Blockchain

In blockchain, Provisional State is a temporary storage space and a logical layer that sits between the stage of initial information admission and the final registration of transactions in the ledger.

The purpose of this temporary storage space is the secure and orderly management of data awaiting finalization — without violating the principles of finality and the integrity of the ledger.

With network support of the AVP-DS capability, the Network Protocol uses the Provisional State layer to store and retain the Execution Permit — before the transaction is registered in the network ledger.

After issuing the Execution Permit, the Network Protocol encrypts it with a per-permit encryption key and retains the encrypted copy in the Provisional State for verification purposes. The designated initial validation nodes, upon receiving the transaction along with the Execution Permit and the per-permit encryption key, are required to decrypt the copy stored in the Provisional State using the received per-permit encryption key, and to verify the authenticity and conformity of the received permit, line by line. After successful verification and completion of the initial validation process, they direct the transaction — along with the Execution Permit and the per-permit encryption key — to the next components, in accordance with the roadmap specified in the Execution Permit.

Other designated components, in the continuation of the validation process, upon encountering a conflict or exceptional condition and requiring re-verification of the permit, use the per-permit encryption key that they have received — along with the transaction and the Execution Permit — from the previously designated component in the permit, to re-decrypt the copy stored in the Provisional State and re-verify the permit.

The retention of the Execution Permit in the Provisional State is temporary, and its lifecycle depends on the status of the related transaction. Accordingly, the removal of the temporary copy of the Execution Permit and its per-permit encryption key is achieved in two ways:

- In the case where the validation process of a transaction results in the registration of an outcome in the network ledger: Regardless of the outcome obtained (successful or unsuccessful), the transaction, along with the Execution Permit, is registered in the final network ledger; then, the encrypted copy of the relevant Execution Permit in the Provisional State and the per-permit encryption key specific to that permit — which was accompanying the transaction — are also removed.
- In the case where the validation process does not result in the registration of an outcome in the network ledger: If the transaction in question is not sent to the network within the specified deadline, or if the transaction is rejected during validation in such a way that its final outcome is not registered in the ledger (such as the rejection of the transaction at the initial validation stage), or after the expiration of the time deadline specified by the Network Protocol, the Execution Permit is removed from the Provisional State, and the per-permit encryption key specific to that permit is simultaneously removed from the operational cycle.

In this manner, the Provisional State plays the role of a temporary and conditional space for supporting pre-finalization verification — without temporary data entering the main ledger or violating the principles of finality and the integrity of the ledger.

### Encryption of the Execution Permit in the Provisional State

To prevent misuse of the information contained within the Execution Permit and to enhance network security against attacks such as Front-Running and Sandwich Attacks, the Network Protocol uses an encryption mechanism for storing Execution Permits in the Provisional State, as follows:

First, simultaneously with the issuance of each Execution Permit, the Network Protocol generates a unique encryption key specific to that permit, and uses it to encrypt the issued Execution Permit.

It then stores the encrypted copy of the Execution Permit — alone and without retaining the encryption key alongside it — in the Provisional State. At the same time, it sends the unencrypted copy of the same Execution Permit, along with the per-permit encryption key specific to that permit, to the requesting wallet.

After signing the transaction, the wallet sends the signed transaction, along with the Execution Permit and the corresponding per-permit encryption key, to the initial validation nodes designated in that same permit.

The nodes designated in the Execution Permit, upon receiving the transaction along with the Execution Permit and the corresponding per-permit encryption key, use the same per-permit encryption key received from the wallet to access the Provisional State and decrypt the Execution Permit related to the transaction stored therein. They then verify the permit received from the wallet against the Execution Permit stored in the Provisional State, line by line.

After successful verification and completion of initial validation, they direct and send the transaction, together with the Execution Permit and the per-permit encryption key — without any new decision-making and solely based on the information in the Execution Permit — to the designated execution domain and execution engine.

Security advantages of this mechanism:

- No early access: Although the nodes have access to the Provisional State space, they cannot decrypt the permit related to themselves, or view its contents, before receiving the signed transaction along with the Execution Permit and the per-permit encryption key from the wallet.
- Simultaneity of decryption with transaction entry: The per-permit encryption key becomes available to the designated nodes only when the signed transaction, along with the Execution Permit and the per-permit encryption key, arrives at the initial validation nodes designated in that same permit. As a result, the contents of the permit become accessible only after the signed transaction has entered the network, and the time window between viewing the permit's contents and executing the transaction becomes so small and limited that it deprives an attacker of the possibility of carrying out an effective attack.
- Restricted access to designated nodes and components: Only the nodes and components designated in the Execution Permit — and only after receiving the transaction along with the Execution Permit and the per-permit encryption key — can access the Provisional State and decrypt and view the contents of the relevant Execution Permit using the received per-permit encryption key.

Other network components that have access to the Provisional State cannot decrypt or, consequently, view the contents of the permits, due to the lack of the per-permit encryption key.

### Monitoring Expected Behavior and Outcome

With network support of the AVP-DS capability, the transaction lifecycle transforms from a simple "send and wait for result" process into a fully verifiable cycle encompassing planning, execution, monitoring, and result validation.

Expected Behavior and Outcome refers to the set of results that, based on the information in the transaction submission request sent from the wallet to the Network Protocol, Network Protocol rules, and the data recorded in the Execution Permit, are anticipated to be observed after transaction execution and before its final recording in the network ledger.

For example, if the wallet submits a request to transfer 10 TRX from account A to account B, the Expected Behavior and Outcome of this transaction would include:

- Deduction of 10 TRX from account A's balance;
- Addition of 10 TRX to account B's balance;
- Execution of the transaction exactly according to the validation path, roadmap, and components specified in the Execution Permit;
- Comparison and monitoring of the validation result obtained from the transaction after the execution engine, with the value recorded in the Execution Permit, by the Network Protocol.

For simple transactions, this behavior is usually highly predictable. Conversely, for more complex transactions—such as smart contract calls—the Expected Behavior and Outcome may involve a set of state changes, outputs, constraints, or conditions defined by the contract itself.

Consequently, for a smart contract call, as with other transactions, the user first sends a request to interact with the contract to the Network Protocol via the wallet, and an Execution Permit is issued for this call by the Network Protocol and sent to the wallet along with the encryption key specific to that permit. The Network Protocol obtains the data required to define the Expected Behavior and Outcome from the contract's recorded content in the network (such as its code and state), previous execution records, and the transaction submission request, and incorporates it into the Execution Permit issuance process.

Internal Calls and the Smart Contract Call Chain

A smart contract call transaction may, during execution, internally call other contracts. In the AVP-DS capability, this entire call chain is considered part of the same transaction and is executed under the same Execution Permit and based on the same roadmap, path, and components specified therein. Internal calls do not receive separate permits and do not follow separate paths; because their independent execution along different paths could itself lead to conflicts in the shared state.

When issuing the permit, the Network Protocol predicts the contracts and accounts that are likely to be involved in the call chain by reviewing the contract's code and state, previous execution records, and the request information, and determines the path and execution engine based on the entirety of them. If other transactions are also related to these same contracts or shared state, they are directed along the same coordinated path in accordance with the shared path policy.

However, if during execution it becomes apparent that the call chain reaches a contract or state that necessitates a different path or components, this event is considered an exceptional condition and, in accordance with Level Two conflict management, its report is sent to the Network Protocol. In this case, the Network Protocol can issue a new Execution Permit for the transaction, and the transaction will be executed along the new path. The execution engine does not independently change the path.

Network Protocol Responsibility

Based on the transaction lifecycle after network support of the AVP-DS capability, the Network Protocol's responsibility does not end with the issuance of the Execution Permit. The Network Protocol monitors the lifecycle of each transaction until its final recording in the network ledger. After the transaction validation is completed in the execution engine and before the transaction is finally recorded in the network ledger, the Network Protocol compares the resulting outcome with the Expected Behavior and Outcome.

- If the observed outcome does not conflict with the Expected Behavior and Outcome, the transaction enters the consensus process and is finally recorded in the network ledger.
- If the execution outcome conflicts with the Expected Behavior and Outcome, the Network Protocol first verifies the Execution Permit and the completed validation stages, and then records it as an exception and prepares an analytical report containing the cause, root cause analysis of the discrepancy, and the handling method. These reports are used to improve policies for defining and monitoring Expected Behavior and Outcome in future transactions and to prevent the recurrence of similar cases.

Investigating the cause of the exception, determining its origin, and deciding on the continuation of the process (including continuation, transaction rejection, or re-validation) is solely the responsibility of the Network Protocol. No consensus, security, or governance rule is modified by this mechanism.

Impact on Resource Allocation

One of the advantages of this model is that the Network Protocol can consider the certainty of the Expected Behavior and Outcome when issuing the Execution Permit. In general:

- Transactions whose Expected Behavior and Outcome are simple, deterministic, and highly predictable can be scheduled with the minimum execution resources required by the Network Protocol.
- Transactions whose Expected Behavior and Outcome are more complex, more sensitive, or dependent on the shared network state can be directed to stronger validation paths or allocated more resources in accordance with Network Protocol policies.

These decisions are fully governed by Network Protocol rules and are reflected in the Execution Permit.

Assisting in Detecting Unexpected Behavior

Monitoring Expected Behavior and Outcome can be an effective tool for detecting unexpected behaviors in the network.

If the final outcome recorded in the ledger deviates from the Expected Behavior and Outcome, the Network Protocol can consider this event as an indicator to investigate issues such as:

- A node exhibiting abnormal behavior;
- Execution errors;
- Synchronization issues;
- Other exceptional conditions.

If the Network Protocol identifies any of the above cases, it first prepares and records an analytical report of the identified deviation for further investigation and record-keeping, and then places the appropriate action regarding the identified unexpected behavior on its agenda.

Re-validation Capability

After the transaction execution is completed in the execution engine and before the final outcome is recorded in the ledger, the Network Protocol compares the "Expected Behavior and Outcome" recorded in the Execution Permit with the outcome obtained from the execution engine.

If the transaction execution outcome in the execution engine conflicts with the Expected Behavior and Outcome recorded in the Execution Permit, the Network Protocol first re-verifies the Execution Permit and, after reviewing the completed validation stages, prepares an analytical report including how it was identified, the cause, the handling method, and the final outcome. It then uses these reports to prevent the recurrence of similar cases in the future, and based on its policies, issues a new Execution Permit for the same request and selects a different validation path. The new permit is issued along with its specific encryption key, and the previous permit and its specific key are removed from the Provisional State.

Comparing the results of independent execution of a transaction along different paths can provide valuable data to the Network Protocol for root cause analysis of the discrepancy, verifying the transaction execution, and detecting abnormal behavior of network components.

Summary

The concept of Expected Behavior and Outcome is one of the complementary capabilities provided by network support of the AVP-DS capability to enhance the observability and auditability of the transaction execution process.

This approach enables the Network Protocol to fully monitor the transaction lifecycle from the moment the transaction submission request is sent from the wallet to the Network Protocol until its final recording in the ledger.

This approach not only enables full monitoring of the transaction lifecycle before the transaction enters the consensus process but also provides a valuable tool for error analysis, policy improvement, increasing validation transparency, and facilitating the investigation of unexpected behavior. As a result, unexpected behavior can be identified more quickly and investigated in accordance with Network Protocol policies, without introducing any changes to the network's consensus mechanism or security model.
___
___
### Full Execution Permit Verification

One of the fundamental principles of the ATHENA architecture is that the Execution Permit is not merely an admission authorization for a transaction. Rather, it is the official, immutable document governing the complete validation and execution lifecycle of that transaction.

At the time of issuance, the Execution Permit is generated based on the current state of the network and the policies defined by the Host Protocol. It records all decisions made by ATHENA for that transaction. Depending on Host Protocol policies, this information may include:

- Transaction type;
- Validation path;
- Initial validator nodes;
- Execution domain;
- Selected execution engine;
- Scheduling policies;
- Permit validity period;
- Security policies;
- Expected behavior;
- And any other parameters required by the Host Protocol.

Simultaneously with permit issuance, a Canonical Copy of the Execution Permit is recorded within ATHENA and serves as the sole authoritative reference for that transaction.


Full Execution Permit Verification Principle

Before any initial validator node begins the transaction validation process, it is required to perform a complete verification of the entire Execution Permit content against the Canonical Copy stored in ATHENA.

This verification is not limited to checking the Permit ID or the validity of the permit signature. Rather, all information recorded within the Execution Permit must match the canonical version without any discrepancy.

In other words, each validator node must verify that:

- The transaction type exactly matches the type for which the permit was issued;
- The validation path remains unchanged;
- The execution domain is the one originally assigned;
- The execution engine is the one originally selected;
- The set of initial validator nodes exactly matches the permit;
- The scheduling and security policies have not been altered;
- The permit validity period has not expired;
- And all parameters defined by the Host Protocol remain identical to the Canonical Copy.

Any discrepancy—even in a single parameter—invalidates the Execution Permit, and the transaction will be rejected before entering the validation and consensus process.


Significance of This Mechanism

In many conventional blockchain architectures, after a transaction is broadcast to the network, its validation path can no longer be independently verified. Subsequent nodes simply accept the results of previous stages without independent validation.

In contrast, ATHENA, by recording the Canonical Copy and requiring initial validator nodes to perform full Execution Permit verification, ensures that the entire validation process proceeds exactly according to ATHENA's original decision. No part of the validation path can be altered between permit issuance and the start of processing.

For this reason, the Execution Permit can be considered the Official Execution Checklist for the transaction—a document that all network components are required to follow precisely during validation and execution.


### Intelligent Transaction Admission and Lifecycle Management

In conventional architectures, after a transaction is broadcast to the network, it enters the validation process, and decisions regarding its execution path are made primarily during the initial stages of processing.

In contrast, ATHENA manages the transaction lifecycle before the transaction enters the network and before the digital signature is ever propagated.

After receiving the Admission Request, ATHENA collects the required information from the wallet and the network according to Host Protocol policies. By analyzing the real-time state of the network—including:

- Available processing capacity of initial validator nodes;
- Status of execution domains;
- Load of parallel execution engines within each domain;
- Transactions currently being processed;
- Execution status of transactions from the same account;
- And other policies defined by the Host Protocol—

and based on the transaction type and the monitored information received from the network, ATHENA determines the most appropriate validation and execution path for the transaction and records all these decisions within the Execution Permit.

The Execution Permit is not merely an admission authorization. It is the document that defines the complete validation and execution path of the transaction—from admission to final ledger recording—and all network components are required to operate according to the information recorded within it and the rules of the Host Protocol.

This approach ensures that every transaction has a defined, verifiable, and pre-planned path before entering the network, preventing sudden congestion, imbalanced load distribution, and inefficient use of processing resources.


### Dynamic Resource Orchestration

One of the most important features of ATHENA is its dynamic management of network resources.

In this architecture, no validation pipeline, execution domain, or execution engine is permanently assigned to transactions.

For each Admission Request, ATHENA independently decides—based on the current state of the network, the type and domain of the transaction, and the Admission Request sent by the wallet—the following:

- Which initial validator nodes should be selected;
- How many groups and, consequently, how many initial validation pipelines are required across the network for this volume of incoming transactions;
- Which Execution Domain the transaction should enter after initial validation;
- Which execution engine, among the parallel engines within that domain, has the lowest processing load.

As a result, the execution path of each transaction may differ from the next, even if both belong to the same type of operation.

This architecture ensures:

- Balanced distribution of processing load across available resources;
- Prevention of hot spots;
- Scalability of operational capacity in proportion to resource growth;
- Elimination of predictability regarding transaction execution paths by nodes or other network actors.

In other words, ATHENA transforms the network from an architecture with unmanaged transaction admission into one with Managed Transaction Admission—an architecture in which transaction volume growth and processing capacity growth can be managed in a coordinated and balanced manner.

### Sender Consistency

ATHENA preserves the logical ordering of transactions for each account without imposing restrictions on other accounts.

If a new request is sent from the same account before a transaction is finalized, ATHENA, in accordance with Host Protocol policies and using the information recorded in the Execution Permit, maintains the logical execution order of transactions for that account.

This restriction applies solely to that account and does not prevent the concurrent processing of transactions from other accounts.

Consequently, while maintaining state consistency for each account, the network's parallel processing capacity is preserved.


### Runtime Monitoring and Adaptive Feedback

ATHENA continuously monitors the operational status of various network components.

This monitoring may include:

- Load of initial validator nodes;
- Load of execution domains;
- Status of parallel execution engines;
- Conflict rate;
- Initial validation time;
- Time to reach consensus;
- Time to reach Finality;
- Re-execution rate;
- Load distribution quality;
- And other performance indicators defined by the Host Protocol.

The purpose of this monitoring is not merely to display network status, but to create a continuous learning cycle for performance improvement.

Whenever a conflict or exceptional condition occurs during validation or execution—such as the absence of an expected outcome or deviation from expected validator behavior—ATHENA prepares an analytical report detailing the cause, the handling approach, and the final outcome, and sends it to the Host Protocol.

This feedback can serve as the basis for refining admission policies, scheduling, node selection, domain selection, execution engine selection, and other Execution Permit issuance policies, reducing the likelihood of similar conflicts or exceptional conditions recurring in the future.

Consequently, ATHENA, without directly altering network policies, enables Continuous Improvement of network performance through operational analysis and feedback to the Host Protocol.

All final decisions remain the authority of the Host Protocol, while ATHENA serves as the intelligent monitoring, analysis, and transaction lifecycle management system.


### Policy-Driven Transaction Lifecycle Management

One of the most important capabilities of the ATHENA architecture is the transformation of the transaction validation process from a static process into a fully policy-driven one.

In conventional architectures, after a transaction enters the network, validators process nearly all transactions using a similar logic, and validation decisions are made during runtime.

In contrast, ATHENA designs the complete execution path of the transaction before it enters the network, based on policies defined by the Host Protocol, and delivers it to the network in the form of an Execution Permit.

For this reason, ATHENA does not decide how a transaction should be validated; rather, it simply enforces the pre‑defined policies established by the Host Protocol.


Execution Policies Are Defined by the Host Protocol

Modern blockchain networks are no longer limited to simple asset transfers.

Depending on the Host Protocol, a network may support various types of operations, including:

- Native coin transfers;
- Token transfers;
- Smart contract execution;
- dApp interactions;
- Staking operations;
- Voting and governance;
- Multi‑signature transactions;
- State‑sensitive operations;
- Cross‑module operations;
- Any new operation type introduced by the Host Protocol in the future.

Clearly, not all of these transactions can be processed with a single validation policy.

For this reason, validation policies for each transaction type are defined solely by the Host Protocol, and ATHENA has no independent decision‑making logic in this regard.


Execution Permit: The Transaction Execution Blueprint

After receiving the Admission Request, ATHENA evaluates the information received from the wallet, the current state of the network, and the Host Protocol policies, and issues the Execution Permit.

The Execution Permit is, in effect, the Execution Blueprint for that transaction.

Depending on Host Protocol policies, this permit may specify:

- The initial validation path;
- The initial validators;
- The Execution Domain;
- The selected execution engine;
- The minimum validation difficulty;
- Scheduling policies;
- Conflict management policies;
- Exception handling policies;
- Monitoring policies or expected behavior;
- Execution constraints;
- And any other parameters the Host Protocol deems necessary.

From this point onward, network components no longer make independent decisions about how to process the transaction; they simply follow the steps defined in the Execution Permit.


Dynamic Routing

One of ATHENA's fundamental differences from conventional architectures is dynamic routing.

In ATHENA, there is no fixed path for any category of transaction.

Even two completely identical transactions may receive different Execution Permits if the network state has changed.

Therefore, the execution path of each transaction is always a function of two factors:

1. The policies defined by the Host Protocol;
2. The real‑time state of the network.

As a result, the network's execution structure can evolve and adapt dynamically without any changes to the consensus algorithm.


Resource Management Based on Transaction Type

The Host Protocol may define different policies for different transaction types.

For example, it may determine that:

- A simple TRX transfer requires only minimal validation resources;
- A specific token transfer requires a different execution domain;
- Smart contract execution requires more validators;
- Minimum validation difficulty varies by transaction type and category;
- Some sensitive transactions should be validated through dedicated paths or with higher difficulty;
- Certain operations should be routed to a specific execution engine;
- Some transactions should be executed in parallel or sequentially and their results compared.

ATHENA does not define these policies; it merely communicates them to the network through the Execution Permit.


Policy Enforcement Verification

One of ATHENA's most important innovations is that the issuance of the Execution Permit is not the end of its responsibility.

ATHENA monitors the execution of the policies defined in the Execution Permit until the transaction is finally recorded in the global ledger.

At this stage, ATHENA verifies whether the network has acted exactly according to the Execution Permit.

This verification may include checking that:

- The validation path was correctly followed;
- All designated validators participated in the validation;
- The execution domain was respected;
- The designated execution engine performed the validation;
- The expected behavior or outcome was correct and no exception occurred;
- And all other policies defined by the Host Protocol were properly enforced.

If any discrepancy is observed, ATHENA registers it as an Exception and sends the necessary report to the Host Protocol.


Transparency in Network Component Behavior

In conventional architectures, once a transaction is broadcast, there is virtually no independent reference to verify whether network components have acted exactly according to protocol policies.

However, in ATHENA, the Execution Permit becomes an official reference for verifying network behavior.

Consequently, any deviation from defined policies is quickly detected and reported by ATHENA to the Host Protocol.

This feature significantly increases the network's transparency, auditability, and observability.


Architectural Principle

ATHENA never decides what a transaction is or how it should be validated.

All execution decisions are made by the Host Protocol.

ATHENA is solely responsible for managing the transaction lifecycle—from receiving the Admission Request, issuing the Execution Permit, managing the execution path, monitoring policy execution, verifying network behavior, and reporting any discrepancies to the Host Protocol.

For this reason, ATHENA can be regarded as a Policy‑Driven Transaction Lifecycle Management Layer—a layer that, without making any changes to the consensus algorithm, security model, or ledger structure, enables intelligent, dynamic, and verifiable management of the complete transaction lifecycle.
___
___
# Removal of Public Transaction Propagation with Network Support of the AVP-DS Capability via Changing Mempool Access from a Shared Memory to a Dedicated Memory

### What is a Mempool?

From a technical perspective, the "mempool" is not a central and unified memory across the entire network; rather, each node (Full Node or validation node) has its own local in-memory data structure, typically kept in RAM, referred to as a Mempool (short for Memory Pool).

In conventional networks, when a transaction is propagated, it is sent to all nodes and copied into the mempool of each individual node. Transactions are distributed in the memory of all network nodes and are observable; in technical literature, this entire distributed layer is referred to as the "Public Waiting Layer" (Public Mempool).

Transaction Admission in Conventional Networks

In conventional blockchain networks, regardless of the consensus algorithm, transaction admission follows a common pattern:

- The wallet signs the transaction;
- The transaction is propagated across the network and placed in the public waiting layer;
- After public propagation, the validation process begins upon the transaction's entry into the network.

In conventional networks, the transaction first enters the waiting pool; therefore, the time of entry is not the same as the time of selection for execution. This model entails the following characteristics:

- Signed transactions enter the network before the allocation of execution resources.
- All transactions are passed around in the nodes' memory and propagated across the entire network.
- The time a transaction enters the network is not the same as the time the validation process begins.
- During periods of congestion, the waiting layer naturally grows.
- The execution path of a transaction remains unknown until validators initiate the validation process.
- All nodes can observe the signed transaction during the waiting period.

Therefore, the public waiting layer in conventional networks is a structural component, not merely an implementation detail.

### Transaction Admission After Network Support of the AVP-DS Capability

With network support of the AVP-DS capability, the transaction lifecycle is redesigned. Instead of allowing a signed transaction to enter the network immediately, the wallet first sends a transaction submission request to the Network Protocol. This request contains the information the Network Protocol needs for admission decision-making. At this stage, no signed transaction exists.

After receiving the required information in the form of a transaction submission request from the wallet—and after monitoring the real-time load and receiving the necessary and supplementary information from network components—the Network Protocol evaluates the current operational state and, by creating a parallel software validation lane that includes the validation roadmap, addressing, routing, and directing the transaction to the designated components (and not the entire hardware capacity), issues the respective Execution Permit in two versions:

- One version is encrypted with the per-permit encryption key and stored in the Provisional State for subsequent verifications.
- The other unencrypted version of the Execution Permit is then sent to the requesting wallet along with its per-permit encryption key.

The Execution Permit contains the transaction's validation roadmap—from the moment the transaction enters the network, including:

- The designated initial validation nodes (and not all initial validation nodes in the network)
- The execution domain
- The least-loaded execution engine among the parallel engines of a domain
- The scheduling policy
- The default conflict management policy
- Monitoring the expected behavior and outcome

—until the transaction is recorded in the network ledger.

Upon receiving the Execution Permit along with the per-permit encryption key, the wallet enables the user to sign the transaction. After the user signs the transaction, the wallet sends the signed transaction along with the Execution Permit and the per-permit encryption key (used to decrypt the stored version of the permit in the Provisional State) directly to the initial validation nodes designated in the Execution Permit, and not to all initial validation nodes in the network.

### Although from a hardware perspective, local memory (mempool) space still exists:

1. This space is no longer public and observable for all network components; rather, it is a private memory dedicated to that specific node.
2. Once the transaction enters this memory, it is not passed around among network nodes.
3. Only the validation nodes designated in the Execution Permit (and not all validation nodes in the network) receive the transaction directly from the wallet in accordance with the Execution Permit.

With network support of the AVP-DS capability, each transaction receives its execution path from the Network Protocol in the form of an Execution Permit prior to entering the blockchain.

Although transactions still utilize the mempool memory space from a hardware perspective, this storage space is no longer public and accessible to all nodes; rather, it becomes a storage space with access dedicated to that specific node.

From the moment the Execution Permit is issued, the wallet already knows:

- Where the transaction must be sent;
- How it will be validated;
- What execution policies will be applied;
- And which validators are responsible for processing it.

Therefore, immediately after signing, the transaction follows its pre-determined execution path. Based on the Execution Permit, each transaction is routed, addressed, and directed along its validation path and designated components (and not the entire hardware capacity of the network).

### Consequences of This Redesign

Removal of the Public Waiting Layer: With network support of the AVP-DS capability, the public waiting layer of transactions is removed from the transaction lifecycle. Transactions no longer wait in a shared pool before execution. First, the hardware capacity and execution resources of the network are assessed; then, parallel software validation lanes are formed, and by determining the allocated hardware capacity, the Execution Permit is issued by the Network Protocol. Validation begins and ends based on the allocated hardware capacity, and not the entire hardware capacity of the network.

Determining the Execution Path Prior to Transaction Creation: Unlike conventional networks, with network support of the AVP-DS capability, the Network Protocol—even before the transaction is signed and enters the network—determines all validation stages, transaction routing, and related components in the form of an Execution Permit and communicates them, along with the transaction, to the designated components and not all network components. From the moment the wallet sends the transaction along with the Execution Permit and the per-permit encryption key to all initial validation nodes designated in the Execution Permit, and upon receipt of the transaction along with the Execution Permit and per-permit encryption key (used to decrypt the stored version of the permit in the Provisional State) by the relevant initial validation nodes, until monitoring the expected behavior and outcome and recording the validation result in the network ledger.

All components designated in the transaction's Execution Permit are required to act without any independent decision-making and strictly in accordance with the stages and components specified in the Execution Permit; such that after passing through each validation stage, the transaction is directed along its dedicated path to the next designated execution component.

Managed Transaction Admission: In conventional networks, the wallet sends the signed transaction, and transaction management is performed after its entry into the network—through scheduling or queuing—and after receipt by network components.

With network support of the AVP-DS capability, this procedure transforms into a managed admission model. Transaction management is performed by the Network Protocol prior to signing and in the wallet. Before the transaction is signed and enters the network, the Network Protocol reviews the real-time state of the network, determines the most appropriate validation and execution path for each transaction, dynamically forms parallel validation lanes based on the volume of incoming requests, and records all these decisions in the Execution Permit.

It then sends the Execution Permit along with its per-permit encryption key to the wallet. After receiving the Execution Permit from the Network Protocol, the wallet allows the user to sign, and after the user signs the transaction, the wallet sends the transaction along with the Execution Permit and the per-permit encryption key (used to decrypt the stored version of the permit in the Provisional State) to all initial validation nodes designated in the Execution Permit.

As a result, the network's input is no longer an unmanaged transaction flow; rather, it is an intelligent, controlled, scheduled, and dynamic flow managed by the Network Protocol.

No Competition or Queuing Among Transactions: Transactions are no longer queued in a public waiting layer. Each transaction, along with the Execution Permit and the per-permit encryption key, enters the network solely through its dedicated execution path specified in the Execution Permit, sent directly from the wallet to all initial validation nodes designated in the permit.

Removal of Unnecessary Public Disclosure: Since signed transactions are not propagated before the allocation of execution resources, unnecessary public disclosure of transaction information is eliminated. The signed transaction becomes visible only to the validation chain responsible for processing that specific transaction.

### Security Implications of the AVP-DS Capability

Transforming the public transaction waiting layer into a local, dedicated buffer specific to each node has important security implications. In conventional blockchain systems, the public mempool acts as a propagation layer where signed transactions are accessible to all network nodes prior to execution.

Researchers have examined various attack scenarios that rely on observing transactions during the waiting period prior to execution and finalization; including Front-Running, transaction copying or replay, and Denial of Service (DoS) attacks and their amplification. Furthermore, another long-term concern exists: when transactions and their signatures are publicly propagated in the network environment—including the mempool, nodes, block producers, validators, and RPC/API providers—they are exposed to widespread observation and recording and are recorded in the network history; as a result, a future attacker might be able to extract the account's private key by analyzing the exposed signature and public key using quantum computers.

With network support of the AVP-DS capability, the conditions required for such attacks are eliminated. Because signed transactions are never placed in a waiting layer with public accessibility:

- There is no public transaction pool to observe;
- No global transaction queue is available for monitoring;
- No structural waiting period exists between public propagation and execution.

Instead, transactions are signed only after receiving the Execution Permit and are sent directly by wallets, along with the respective Execution Permit and the per-permit encryption key, to all validators designated in the Execution Permit.

In this design, the public disclosure surface resulting from conventional designs based on public/shared mempools no longer exists; because the mempool in this design is a private, local memory specific to each node, not a public memory accessible to all network nodes.

### Native Compatibility

As a result, with network support of the AVP-DS capability and the transformation of the publicly accessible mempool into local and dedicated buffers specific to each node, the wallet sends the transaction along with the Execution Permit and the per-permit encryption key (used to decrypt the stored version of the Execution Permit in the Provisional State) directly to all initial validation nodes designated in the Execution Permit. In this state, the structural exposure layer caused by the shared mempool no longer exists; while the native consensus, execution engine, and security model of the Network Protocol remain intact.

### Summary of the AVP-DS Capability

With network support of the AVP-DS capability, the transaction waiting layer—which was previously a structural component and a public, accessible memory for all network nodes—is transformed into a dedicated buffer specific to each node. Following this change, instead of being passed around in the mempool until reaching the entire network, the transaction is sent directly by the wallet to all initial validation nodes designated in the Execution Permit.
___
___
# Transaction Lifecycle After Network Support of the AVP-DS Capability

With network support of the AVP-DS capability, the lifecycle of each transaction begins from the moment the transaction submission request is sent by the wallet to the Network Protocol, and continues until the comparison and monitoring of the "expected behavior or outcome" recorded in the Execution Permit against the validation result — and then the registration of the final transaction result in the network ledger.

In this framework, the Network Protocol is the authority for issuing Execution Permits to route transactions into the network and place them on the authorized validation path — on a per-transaction basis.

The instructions concerning the execution path, the relevant authorized components, and the validation conditions — including conflict management at two levels (prevention of conflict before the transaction is sent, and management of conflict after the transaction is sent to the network if identified by the relevant validation components) — are issued within that same permit, on a per-transaction basis, by the Network Protocol.

After the components and validation path are determined and the Execution Permit is issued on a per-transaction basis, all relevant and designated components are required to follow the path and instructions of that same permit, and no designated execution component is permitted to independently alter the path or the designated decisions.

### Phase 1: Initial Preparation, Data Collection, and Submission of the Transaction Request to the Network Protocol

The user enters the required transaction information in the wallet. Depending on the type of operation, this information may include:

- Sender address
- Receiver address
- Asset amount
- Asset type (TRX, TRC-20, NFT, etc.)
- Smart contract invocation
- Contract parameters
- Any other information that the Network Protocol, in accordance with its policies, deems necessary.

After completing the information, the wallet displays the transaction summary on the confirmation screen for user review before signing.

At this stage, and before the user is authorized to sign the transaction, the wallet prepares a transaction submission request (Admission Request) — containing the information required under the rules and requirements of the Network Protocol — and sends it to the Network Protocol.

After receiving the transaction submission request from the wallet, the Network Protocol evaluates the request and, after reviewing the real-time network state and its own policies, issues an Execution Permit if approved.

Only after receiving the Execution Permit from the Network Protocol is the wallet authorized to allow the user to sign the transaction. As a result, no signed transaction is created or sent before receiving the Execution Permit, and all transactions, from the outset, are routed — based on the execution path determined by the Network Protocol — to the relevant components designated by their own dedicated Execution Permit.

### Phase 2: Managed Admission

Network support of the AVP-DS capability replaces "unmanaged admission" with "managed admission."

In many current networks, wallets send transactions to the transaction-hosting network without any awareness of the real-time state. After transactions are propagated and enter the network, networks make transaction management possible only after entry, through scheduling or queueing.

Network support of the AVP-DS capability makes transaction management possible not after they are sent, but before sending, at the wallet. Before signed transactions enter the network, the Network Protocol:

- Reviews the real-time network state.
- Then determines the most appropriate validation and execution path for that transaction.
- Based on the volume and number of incoming transaction requests, dynamically forms parallel validation lanes and communicates them, on a per-transaction basis, to the relevant components within the Execution Permit.
- The Execution Permit contains the validation-related components, on a per-transaction basis for each incoming transaction, and designates the relevant validation components for each transaction based on the dynamic validation lanes, in proportion to the volume of incoming transaction requests.
- Each transaction uses only the designated validation path and the designated validation components — not a public path, and not the entire network's capacity for validation — in accordance with the Execution Permit issued by the Network Protocol.

As a result, transaction management becomes possible before the signed transaction enters the network, through the interaction of the wallet with the Network Protocol — such that the issuance of the Execution Permit and the determination of the transaction path occur before signing the transaction and before sending the transaction to the network.

Thus, the network's input is no longer an unmanaged stream of transactions, but an intelligent, controlled, scheduled, dynamic flow in the hands of the Network Protocol.

### Phase 3: The Execution Permit

The Execution Permit is not merely an admission authorization; it is the dedicated roadmap of each transaction, in which the Network Protocol determines addressing, routing, and transaction direction — from the moment the wallet sends the transaction submission request to the Network Protocol until registration in the ledger. This permit is the interface between the Decision Layer and the Execution Layer, and it conveys the dedicated instructions of each transaction to the relevant components.

The Execution Permit includes the following:

- Designation of the components responsible for validation (only the designated components, not the entire network capacity)
- The policy for preventing potential conflicts at two levels (before and after network entry)
- Designation of the signature algorithm
- Transaction information: sender and receiver addresses, asset type and amount, expected behavior or outcome, relevant validators, initial validation lane, execution domain and the least-loaded parallel execution engine, and other parameters required by the Network Protocol

Addressing and routing are performed exclusively for each transaction and are not limited to a single public, fixed path for validating all incoming transactions. All relevant components designated in the Execution Permit, on a per-transaction basis, are required to follow the path and instructions specified therein and to advance the process in accordance with the Network Protocol's decisions.

After the Execution Permit is issued, the Network Protocol encrypts it with a per-permit encryption key and retains the encrypted copy in the Provisional State. It then sends a copy of the Execution Permit along with the corresponding per-permit encryption key to the requesting wallet, so that the relevant components can decrypt the copy retained in the Provisional State, and verify the authenticity and conformity of the received permit.

After receiving the Execution Permit, the wallet enables the user to sign the transaction and, after signing, sends the transaction — along with the Execution Permit and the per-permit encryption key — to the designated initial validation nodes.

### Phase 4: Transaction Signing After Receiving the Execution Permit

After the user signs the transaction, the wallet sends the transaction — along with the unencrypted copy of the Execution Permit and the per-permit encryption key specific to that permit — to the initial validation nodes designated in the Execution Permit.

The relevant validation components in the network use the per-permit encryption key — which was sent along with the transaction — to decrypt the encrypted copy of the Execution Permit stored in the Provisional State, for the purpose of verifying the submitted permit.

Therefore, after receiving the permit, the wallet enables the user to sign the transaction and sends the transaction, along with the Execution Permit and the per-permit encryption key, to the initial validation nodes specified in the Execution Permit.

### Phase 5: Direct Submission of the Transaction to the Initial Validation Nodes

First, based on the Network Protocol's instructions, the wallet prepares the transaction submission request along with the required information and sends it to the Network Protocol for evaluation.

After receiving the Execution Permit from the Network Protocol, the wallet enables the user to sign the transaction. After the user signs the transaction, the wallet sends the signed transaction — along with the Execution Permit and the per-permit encryption key — directly to the initial validation nodes designated in that same received permit.

In this manner, the signed transaction does not enter any public transaction queue or public waiting layer and will enter the validation process via the dedicated path determined in the Execution Permit.

### Phase 6: Full Verification of the Execution Permit

Before validation begins, the initial validation nodes are required to decrypt the encrypted copy of the Execution Permit retained in the Provisional State using the per-permit encryption key received from the wallet, and then verify the full contents of the Execution Permit received from the wallet against that decrypted copy, fully and line by line, within the framework of the Network Protocol.

This verification covers all components of the permit. In the event of any discrepancy, the transaction is rejected and the relevant report is sent to the Network Protocol.

Upon successful verification and confirmation of the Execution Permit and its full conformity with the decrypted copy from the Provisional State — given that the complete roadmap of addressing, routing, and the components responsible for validation has been fully determined and specified in the Execution Permit — all relevant and designated components are required to follow exactly the instructions recorded in that same permit, without independent decision-making regarding the path or assigned duties.

### Phase 7: Initial Validation

The initial validation nodes designated on a per-transaction basis, in accordance with the Execution Permit issued by the Network Protocol, receive the transaction along with the Execution Permit and the per-permit encryption key. They then use the per-permit encryption key to decrypt the encrypted copy retained in the Provisional State, and complete full line-by-line verification of the received permit against the decrypted copy. After completing this verification, they perform preliminary checks based on the items specified by the Network Protocol — including the following:

- Digital signature validity
- Transaction structure
- Account balance
- Request validity
- Any other checks defined by the Network Protocol

After successful completion of initial validation, the designated nodes send the transaction, together with the Execution Permit and the per-permit encryption key, to the specified execution domain and, from among the set of parallel execution engines in that domain, to the exact execution engine specified in the Execution Permit.

Each component associated with the validation of a specific transaction, in accordance with the Execution Permit issued by the Network Protocol on a per-transaction basis, is required — after successfully completing its own stage — to deliver the transaction, without any independent decision, strictly in accordance with the instructions recorded in the Execution Permit, to the next relevant component.

### Phase 8: Routing the Transaction to the Execution Engine Designated in the Execution Permit

After completion of initial validation, the transaction is routed exactly in accordance with the Execution Permit to the designated execution domain and the specified execution engine.

No new decision is made by any node at this stage.

Network members are not authorized to make independent decisions at any stage of validation; all stages must be performed exactly in accordance with the Execution Permit.

### Phase 9: Transaction Execution

After successful completion of initial validation and submission of the transaction to the execution engine designated in the Execution Permit, the execution engine executes the transaction in accordance with the Network Protocol's rules and instructions. All state transitions, smart contract executions, and other native network logic are performed at this stage.

Throughout this process, no component of the network is permitted to choose a new path or execution engine; all stages must be performed exactly in accordance with the instructions recorded in the Execution Permit.

### Phase 10: Monitoring the Expected Behavior or Outcome, Before Ledger Registration

After completion of transaction execution in the execution engine and before the final result is registered in the ledger, the Network Protocol compares the execution result with the "expected behavior or outcome" recorded in the Execution Permit.

If the result matches the expected behavior or outcome, the transaction is sent to complete the consensus process and be finally registered in the ledger.

If it does not match, the Network Protocol:

- First verifies the transaction's Execution Permit and reviews the validation stages that have been completed.
- Then prepares and maintains an analytical report containing the result of the Execution Permit verification, the completed validation stages, information about the identified discrepancy, and the actions taken to manage or resolve it, with the aim of preventing the recurrence of similar conflicts.

Decision-making regarding how to manage the discrepancy — including continuing the process, rejecting the transaction, re-validation, or any other decision — rests exclusively with the Network Protocol.

### Phase 11: Conflict Management

With network support of the AVP-DS capability, conflict management is part of the Network Protocol's decision-making process and is performed at two levels:

Level One — Prediction and Prevention of Conflict, Before the Transaction Enters the Network

By reviewing the real-time network state, the information received from the wallet, its own policies, and the experience of past conflicts, the Network Protocol predicts and assesses the likelihood of conflict and determines preventive measures and the appropriate conflict management policy in each transaction's Execution Permit.

Level Two — Identification and Management of Conflict, After the Transaction Enters the Network

The execution components designated in the Execution Permit, upon identifying a conflict or exceptional condition, decrypt the encrypted copy retained in the Provisional State using the per-permit encryption key, verify the Execution Permit against the decrypted copy, review the completed validation stages, and send the verification report and conflict information to the Network Protocol. Decision-making regarding continuing the process, re-execution, issuing a new permit, changing the path, or rejecting the transaction rests exclusively with the Network Protocol, and all relevant components are required to execute its instructions.

Analytical Report and Prevention of Conflict Recurrence

For each identified conflict, the Network Protocol prepares and maintains an analytical report containing the cause, the manner of identification, the actions taken, and the final outcome. This information is used to improve the policies for issuing Execution Permits, selecting the validation path, validation nodes, domain, and execution engine, and to prevent the recurrence of similar conflicts in future transactions.

### Phase 12: Consensus and Finality

The AVP-DS capability is not designed to change or replace the network's fundamental mechanisms, including consensus layers, protocol policies, or core validation rules.

Through the separation of the Decision Layer from the Execution Layer, this capability enables the dynamic use of new capacities, increases validation capacity through parallel paths, manages the transaction from the request stage in the wallet to registration in the ledger, and prevents conflicts before the transaction enters the network.

Throughout all these stages, the Network Protocol remains the exclusive decision-making authority, and the components relevant to each transaction follow the instructions issued in the Execution Permit. Therefore, supporting networks can utilize their resources and capacities in a coordinated, dynamic, intelligent, and scalable manner, without requiring changes to the fundamental mechanisms, consensus, or core rules of the network.

### Phase 13: Registration in the Network Ledger (Transaction Information Alongside the Execution Permit)

In many conventional architectures, when a transaction is registered in the network ledger, only items such as the final transaction result, the signature hash, the sender and receiver addresses, the amount and type of asset, and other public information are visible — and no information about the validation path and relevant components, including the responsible nodes or the execution engine, is present.

In contrast, with network support of the AVP-DS capability, it becomes possible to fully reconstruct the validation path, in addition to the public information. This transparency — the ability to reconstruct and audit — is among the benefits of network support of AVP-DS.

For this reason, the network must store the Execution Permit or the verifiable cryptographic commitment associated with the transaction, along with the other public transaction information, in the network ledger. The per-permit encryption key is never recorded in the ledger and is removed from the operational cycle after the transaction and the Execution Permit are registered in the network ledger.

This information enables independent auditing, reconstruction of the transaction's execution path, verification of the performance of network components and monitoring of the behavior of the relevant components (including nodes and engines), evaluation of validator performance, and analysis of the validation process — even years after finality.

### Overview of the Transaction Validation Path in the Network After Support of the AVP-DS Capability

```

┌───────────────────────────────────────────────────────────┐
│           1: User: Decision to submit a transaction                  │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│           2: Wallet: Initial transaction preparation                 │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 3: Wallet: Data collection and sending the transaction               │
│             request to the Network Protocol                          │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 4: Network Protocol: Receiving the transaction request               │
│                   from the wallet                                    │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 5: Network Protocol: Receiving required information                  │
│               from network components                                │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 6: Network Protocol: Adopting the required policy for                │
│           potential conflict prevention                              │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 7: Network Protocol: Creating parallel software                      │
│ validation lanes by selecting components and                         │
│ determining the transaction validation path                          │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│     8: Network Protocol: Issuing the Execution Permit                │
└────────┬─────────────────────────────────────────┬────────┘
          │                                                 │
          ▼                                                ▼
┌────────────────────┐         ┌──────────────────────────────────────┐
│ 9: Network Protocol    │        │ 10: Network Protocol: Sending the           │
│ Storing an encrypted   │        │ unencrypted Execution Permit along          │
│ copy of the            │        │ with the per-permit encryption key          │
│ Execution Permit       │        │ to the wallet                               │
│ using the              │        └─────────────────┬────────────────────┘
│ per-permit             │                             │
│ encryption key in      │                             ▼
│ the Provisional        │     ┌──────────────────────────────────────┐
│ State                  │     │ 11: Wallet: Displaying the                  │
└────────┬───────────┘     │ transaction signing window to the           │
          │                    │ user and signing the transaction            │
          │                    └─────────────────┬────────────────────┘
          │                                         │
          │                                         ▼
          │                     ┌──────────────────────────────────────┐
          │                     │ 12: Wallet: Sending the signed              │
          │                     │ transaction along with the Execution        │
          │                     │ Permit and the per-permit encryption        │
          │                     │ key to the initial validation nodes         │
          │                     │ designated in the Execution Permit          │
          │                     └─────────────────┬────────────────────┘
          │                                          │
          │                                          │
          └───────────────────┬────────────────┘
                                 │
                                 ▼
┌───────────────────────────────────────────────────────────┐
│ 13: Initial Validation Nodes: Using the received                     │
│ per-permit encryption key along with the Execution Permit and the    │
│ signed transaction from the wallet, they first decrypt               │
│ the Execution Permit copy stored in the Provisional                  │
│ State, and then verify the Execution Permit received                 │
│ from the wallet line-by-line against the decrypted                   │
│ version in the Provisional State                                     │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 14: Initial Validation Nodes: After successful                       │
│ verification and completion of initial validation, they              │
│ send the transaction to the execution domain and                     │
│ execution engine designated in the Execution Permit                  │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 15: Execution Engine: Upon receiving the transaction                 │
│ along with the verified Execution Permit and the                     │
│ per-permit encryption key, executes and confirms the transaction     │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 16: Network Protocol: Monitoring the expected behavior               │
│                       and outcome                                    │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 17: Network: Transaction entering the consensus process              │
└─────────────────────────────┬─────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────┐
│ 18: Network: Recording the transaction and Execution                 │
│ Permit in the network ledger, removing the per-permit                │
│ encryption key accompanying the transaction, and also removing the   │
│ Execution Permit stored in the Provisional State                     │
└───────────────────────────────────────────────────────────┘

```
___
___
# Threat Model

The ATHENA threat model defines the security assumptions, scope of responsibility, and the types of threats this architecture is designed to manage or mitigate.

ATHENA is a transaction lifecycle management, admission, scheduling, routing, and execution monitoring layer. It does not replace the Host Protocol's consensus algorithm, validation rules, or security model.

Therefore, the ultimate security responsibility of the network remains with the Host Protocol.

### Security Assumptions

This architecture is designed based on the following assumptions:

- The Host Protocol's consensus algorithm is correctly implemented.
- The Finality mechanism is valid.
- Validators operate according to Host Protocol rules.
- Cryptographic algorithms and digital signatures are valid.
- Authentication mechanisms and network access controls are in place.

If any of these assumptions are violated, the responsibility for managing them falls to the Host Protocol.

### Threats Addressed by ATHENA

1. Congestion Attacks

Sending a large volume of Admission Requests to reduce network efficiency.

ATHENA mitigates these attacks through intelligent admission management, dynamic scheduling, and balanced load distribution among initial validators, execution domains, and parallel execution engines.

2. Mempool Observation Attacks

In many networks, signed transactions are placed in a public mempool before entering consensus, where they become observable.

In the ATHENA architecture, there is no public mempool.

Transactions are only sent directly to designated initial validators after the Execution Permit has been issued and the user has signed the transaction.

Consequently, the attack surface arising from the public observation of pending transactions is significantly reduced, and the exploitable time window is completely eliminated.

3. Malicious Full Node Behavior

A malicious Full Node may attempt to:

- Send the transaction through a different path.
- Ignore the Execution Permit instructions.
- Alter the order of execution stages.
- Send incorrect information to other components.
- Refuse to forward the transaction to the next network component.

Since all network components are required to verify the Execution Permit against the Canonical Copy, any deviation from the designated path is immediately detectable. The Canonical Copy mechanism, as an immutable reference, enables the detection of malicious behavior even when attempts are made to disregard the permit.

4. Malicious Initial Validator Behavior

Examples of such behavior include:

- Intentional delays
- Non-responsiveness
- Submitting invalid results
- Incomplete participation in validation
- Failure to follow Execution Permit instructions

These behaviors are recorded during ATHENA's monitoring process and reported according to Host Protocol policies. Any deviation from the designated validation process is also detectable through full Execution Permit verification.

5. Unauthorized Path Modification

After the Execution Permit is issued, no network component is permitted to independently change:

- The validation path
- The execution domain
- The execution engine
- Or the order of execution stages.

Any independent modification will be detected during Execution Permit verification and will result in transaction rejection and a violation report.

6. Unexpected Behavior or Outcome

After the transaction is finally recorded in the global ledger, ATHENA compares the actual execution result with the "expected behavior or outcome" recorded in the Execution Permit.

If any discrepancy is observed, ATHENA sends a report to the Host Protocol so that it can decide how to handle the situation according to its defined policies.

7. Attacks Based on Fixed Structures

In many architectures, fixed validation structures can become targets of coordinated attacks.

In ATHENA, the selection of initial validators, execution domains, and execution engines is performed dynamically for each transaction based on Host Protocol policies.

This feature reduces the likelihood of forming predictable structures.

### Threats Outside the Scope of ATHENA's Responsibility

The following remain outside ATHENA's scope of responsibility and are managed by the Host Protocol or the network infrastructure:

- Attacks against the consensus algorithm
- 51% attacks or similar
- Cryptographic algorithm weaknesses
- Theft of user private keys
- Compromise of user wallets
- Network layer attacks
- Physical attacks against node infrastructure
- Operating system or hardware defects

### Separation of Responsibilities Principle

ATHENA is responsible for:

- Transaction admission management
- Execution Permit issuance
- Scheduling
- Transaction routing
- Initial validator selection
- Execution domain selection
- Execution engine selection
- Exception management
- Monitoring expected behavior or outcomes
- Monitoring the correct execution of policies defined in the Execution Permit
- Transaction lifecycle oversight

In contrast, the following responsibilities remain with the Host Protocol:

- Final validation
- Consensus algorithm execution
- Block production
- Finality
- Global ledger management
- Fundamental network security

### Summary

ATHENA significantly reduces the attack surface at the transaction admission and processing layer by:

- Eliminating the public mempool,
- Implementing intelligent admission management,
- Issuing Execution Permits,
- Deterministically defining the transaction execution path,
- Continuously verifying permits,
- Managing exceptions,
- Monitoring expected behavior or outcomes,
- And overseeing the execution of defined policies.

However, ATHENA is not responsible for the consensus algorithm or the fundamental security of the Host Protocol. It serves solely as a complementary layer that manages and controls the transaction lifecycle—from the initial admission request through to final monitoring after ledger recording.
___
___
# The AVP-DS Capability Vision for the Network

"The true innovation of AVP-DS is not parallel validation of transactions itself; it is determining the routing path of transactions across the network for their confirmation, based on addressing and the components specified in the permit issued by the Network Protocol.

This capability is one of the fundamental capabilities in blockchain networks built on the separation of the Decision Layer from the Execution Layer."

Separation of the Decision Layer from the Execution Layer

One of the fundamental principles of the AVP-DS capability is the separation of the Decision Layer — responsible for deciding the routing and confirmation path of a transaction — from the Execution Layer, i.e., the components responsible for validating and confirming the transaction in the network.

In many conventional blockchain architectures, once a transaction enters the network, its validation and execution path is determined gradually and based on the internal state of the network. In this model, routing decisions are made concurrently with the transaction's entry into the network and throughout the processing stages, and different network components may make independent decisions at different stages of the process.

The AVP-DS capability fundamentally changes this approach.

In AVP-DS, before the transaction enters the network, its complete validation and execution path is determined. This path is recorded in the form of an Execution Permit, which enters the network alongside the transaction. From that moment onward, all network components are required to follow the path defined in the Execution Permit, and no independent decision-making regarding path changes or re-routing of the transaction is permitted outside the framework of the permit.

In other words, the Execution Permit is the execution blueprint of the transaction, and all network components act according to this blueprint and within the framework of the Network Protocol's rules.

### The Intelligent Decision Layer

In this approach, the AVP-DS capability provides a foundation for intelligent management and routing of transactions, enabling the determination of the appropriate execution path before the transaction enters the network.

Based on the transaction's information, the real-time state of the network, and the policies of the Network Protocol, this mechanism determines the following:

- Which initial validator nodes should perform the validation.
- Which execution domain the transaction should enter.
- Which parallel execution engine within that domain should execute the transaction.
- How the complete lifecycle of the transaction — from admission to final registration in the ledger — should proceed.

As a result, the transaction's path is determined before it enters the network, and network components subsequently act in accordance with the path specified in the Execution Permit.

### Independence from Redesign and Rework

The innovation of AVP-DS is not the creation of parallel execution engines or an increase in the number of initial validator nodes.

The core innovation is providing the capability to route transactions from the moment of entry to registration in the ledger, based on the permit issued by the Network Protocol.

For this reason, the AVP-DS capability is not limited to a specific number of initial validator nodes, execution domains, or parallel execution engines.

Whenever the Network Protocol adds new processing capacity to the network, AVP-DS can, through the addressing mechanism and the permits issued, utilize that capacity within parallel validation and execution paths.

Therefore, AVP-DS imposes no fixed ceiling on the expansion of validation and execution paths.

As network capacity grows, the possibility of dynamic and targeted expansion of parallel validation paths — through the use of additional parallel execution engines within the same domain — is provided, and this new capacity is used, based on the issued permits, to route transactions, without any need to rework the logic or base design of the network.

### Intelligent Addressing: The Core of AVP-DS

Although this capability encompasses concepts such as the Execution Permit, execution domains, parallel execution engines, conflict management, and auditing, all of these capabilities rest on a single foundational concept:

Intelligent addressing of the transaction, before it enters the network.

In essence, AVP-DS determines the execution path of each transaction before it enters the network — based on addressing and the permit issued by the Network Protocol — and communicates this path to the selected network components through the Execution Permit.

From this perspective, the Execution Permit is the precise address of the transaction and the complete navigation map of its movement within the network.

This foundational concept enables the creation of parallel validation and execution paths, conflict management, auditing, full coverage of the transaction lifecycle, and effective utilization of the network's new capacities.

### The Principle of Neutrality

The AVP-DS capability makes no change to the network's consensus mechanism, governance model, ledger structure, account model, or native validation rules.

Furthermore, this capability imposes no new role on network components.

All decisions regarding consensus, block production, finality, and the policies of transaction validation and execution remain exclusively under the authority of the Network Protocol.

The role of AVP-DS is to provide the ability to determine the appropriate execution path for each transaction before it enters the network, and to keep network components aligned with the determined path throughout the transaction's lifecycle.

### Here is the English translation of your exact text, preserving its structure and emphasis, and now also including the closing six-line statement.

### Why AVP-DS?

"It is more rational," because instead of adding new mechanisms, it does not change the native rules and laws of the Network Protocol. The Execution Permit — encompassing everything from addressing and the designation of initial validators, to the determination of the domain and the least-loaded execution engine from among the execution engines of a domain, to the registration of the transaction in the ledger — is entirely regulated by the Network Protocol and within the framework of existing policies, and no external component or new intermediary layer is imposed on the network. This means minimal implementation cost, maximal compatibility, and the elimination of any risk of incompatibility through the use of existing mechanisms.

"It is more intelligent," because the decision regarding the path of each transaction is made before the transaction enters the network — not after entry, amid crowded queues and unnecessary competition. This means that, instead of "reacting to existing conditions or conflicts," "predicting --- determining conditions or conflicts" takes place. As a result, architectural bottlenecks are eliminated, public queues disappear, and load distribution occurs in real time, based on addressing and the correct and optimal use of existing capacities.

"It is more scalable," because — it is not limited to a specific number of nodes, domains, or execution engines — based on the Execution Permit issued by the Network Protocol, each transaction is routed to the validation nodes and the least-loaded execution engine from among the execution engines of a domain. As a result, each transaction uses only the components specified in the Execution Permit — not the entire validation capacity of a network. In this manner, the allocation of resources and the execution of each transaction are carried out based on the decision of the Network Protocol. Whenever new capacity is added to the network, the AVP-DS capability causes the Network Protocol to utilize that capacity, without any change to the base logic, within parallel validation and execution paths, and to use the new capacity toward increasing the volume of validated transactions. This means that the growth of network capacity and the increase in transaction confirmation capacity proceed simultaneously and in the same direction as the increase in incoming transactions to the network.

"It is more dynamic," the AVP-DS capability provides the Network Protocol with the possibility of dynamic decision-making regarding the routing of transactions, the selection of the components responsible for execution from among all execution components, and the determination of the signature algorithm to be used. This dynamism can be expressed in four principal dimensions:

- Dynamic formation of parallel validation lanes: the Network Protocol, based on the volume of incoming transactions, forms parallel validation lanes in real time. This means that the number of active lanes is determined in real time and in proportion to the actual load of the network — not in advance or in a fixed manner. As a result, the network can, with any change in incoming volume, without the need for redesign or rework of the validation structure, align itself with the new conditions.
- Dynamic routing: the Network Protocol, through the Execution Permit, specifies the routing path of each transaction and the components designated for its validation and execution. This decision is made in real time and based on the current state of the network, and is recorded in the Execution Permit.
- Dynamic execution: the Network Protocol, by monitoring the load of the parallel engines of a domain at the moment of issuing the Execution Permit, routes and sends the transaction to the least-loaded execution engine from among the parallel execution engines of a domain. Hence, considering the volume of incoming transactions and the available processing capacity, the possibility of expanding and adjusting parallel validation paths for the network is always provided.

Dynamic selection of the signature algorithm: the principle of separating the Decision Layer from the Execution Layer provides the possibility for the network to simultaneously support multiple signature algorithms, without being obligated to use all supported algorithms simultaneously. Initially, new signature algorithms are added to the set of algorithms under the network's software support, according to the required security levels, the functional characteristics of each algorithm, and the operational conditions of the network. Then the Network Protocol, taking into account the strengths and weaknesses of the supported algorithms and based on real-time monitoring of the conditions and needs of the network, at the time of issuing the Execution Permit for each transaction, determines the permitted algorithm for signing that transaction and specifies it in the Execution Permit. The wallet also signs the transaction in accordance with the Execution Permit and using that same determined algorithm, and sends it to the network.

In this approach, the decisions regarding addressing, routing and directing, and the selection of the transaction's signature algorithm are determined by the Network Protocol in the form of the Execution Permit for each transaction, and are communicated to the wallet and the execution components. In this manner, the AVP-DS capability causes the network — without any change to the consensus mechanism, the ledger structure, the account model, or the native validation rules — to provide the possibility of a more dynamic compatibility of the transaction execution process with the capacities, security requirements, and operational conditions of the network.

### The AVP-DS capability means:

network growth,
the addition of hardware and software capacities,
and an increase in the capacity to confirm transactions through parallel validation paths;

all of this through the separation of the Decision Layer from the Execution Layer, without any change to the fundamental mechanisms of the network, and through the routing and addressing of each transaction based on the Execution Permit issued by the Network Protocol.
___
___
