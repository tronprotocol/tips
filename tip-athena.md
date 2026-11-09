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

After receiving the Execution Permit, the wallet grants the user permission to sign the transaction and then sends the transaction, along with the permit, to the initial validation nodes designated in the permit.

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
- Storing a copy of the Execution Permit in the Provisional State, under the control and supervision of the Network Protocol, in order to provide the possibility of verification in the network

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

1. The wallet, based on the permit, sends the signed transaction to the related initial validation nodes designated.
2. The initial validation nodes, as their first action, verify the received permit against the copy stored in the Provisional State, line by line, and after completing the initial validation, direct and send the transaction — without any new decision-making and solely based on the information in the Execution Permit — to the designated execution domain and execution engine.
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

After issuing the Execution Permit, the Network Protocol retains a copy of it in the Provisional State for verification purposes, so that the initial validation nodes or the relevant components identifying potential conflicts can verify the authenticity and conformity of the received permit, line by line.

The retention of the permit in the Provisional State is always temporary and time-bound.

- After successful validation, the transaction, along with the Execution Permit, is registered in the final network ledger, and then the temporary copy of the Execution Permit is removed from the Provisional State.
- If the transaction in question is not sent within the specified deadline, or the validation process does not reach a final outcome, the permit is removed from the Provisional State after the expiration of the time window specified by the Network Protocol.

In this manner, the Provisional State plays the role of a temporary and conditional space for supporting pre-finalization verification — without temporary data entering the main ledger or violating the principles of finality and the integrity of the ledger.
___
___
### Fundamental Principle of ATHENA Architecture

One of the most important distinctions between ATHENA and many existing architectures is that in this architecture, there are no pre‑formed or permanent validator groups or execution groups.

Each Execution Permit is created independently, based on the current state of the network, Host Protocol policies, the capacity of validator nodes, the capacity of execution engines, and the specific characteristics of the transaction request.

As a result, ATHENA first dynamically selects the initial validator nodes and forms an initial parallel validation pipeline from them. It then determines the appropriate execution domain and selects the least‑loaded execution engine among the parallel engines operating within that domain. All these decisions are recorded in the Execution Permit, which defines the complete validation and execution path for the transaction.

Therefore, in the ATHENA architecture, validation pipelines, execution domains, and selected engines are not fixed architectural components; they are the result of ATHENA's dynamic, real‑time decision‑making at the time of Execution Permit issuance.

Since this process is performed independently for each request, the composition of initial validator nodes, the execution domain, and the selected engine may differ from one transaction to the next. Consequently, no validator node or execution engine can predict permanent membership or anticipate its presence in a specific validation or execution path in advance.

The Execution Permit is not merely an admission authorization; it is the authoritative document that defines the complete validation and execution path of the transaction—from the admission stage to final recording in the global ledger. All network components are required to act in accordance with the information recorded in this permit and the policies defined by the Host Protocol.

Furthermore, before the transaction enters the network, ATHENA analyzes the real‑time network state and leverages knowledge gained from past conflicts to select the most appropriate validation and execution path, thereby reducing the likelihood of conflicts from the outset. This feature transforms conflict management from a reactive process into a proactive one.

For this reason, the ATHENA architecture can be regarded not only as a transaction lifecycle management system but also as the first known framework to introduce the concept of proactive conflict management—based on the Execution Permit and performed before the transaction enters the network—in a public blockchain.

### Sequential Transaction Processing

Preserving transaction order is one of the important security components of the TRON network. With the introduction of ATHENA into this network, this advantage remains fully intact.

Based on this mechanism, ATHENA establishes a defined sequential relationship between consecutive transactions from the same account, according to Host Protocol policies. This ensures that a subsequent transaction or a reconstructed transaction cannot bypass the original transaction simply by modifying the fee, changing the submission path, or reaching a node earlier.

The purpose of this mechanism is to create a deterministic and verifiable order for the admission of related transactions into the validation and processing pipeline.

1. Enforcing Order at the Admission Layer

In the ATHENA architecture, transaction ordering is enforced at the Admission Layer through the Execution Permit.

When a transaction from a source account enters the admission process, ATHENA records the processing state of that account.

Until the previous transaction reaches the required state for passing the Admission stage—according to Host Protocol policy—ATHENA will not issue a new permit for the next transaction from the same account.

As a result, an account cannot bypass its previous transaction by submitting a new transaction, nor can it cause the new transaction to enter the validation path earlier.

This rule applies to both individual transactions and Bundles.

2. Independence from Submission Type

Processing order is not determined by submission type.

This means that:

- An individual transaction cannot overtake a previous Bundle.
- A new Bundle cannot overtake a previous individual transaction.
- A Bundle cannot gain priority over a previous request from the same account simply because it contains more transactions or has a different fee.

Therefore, the sequential relationship between requests from the same account is independent of whether the request is submitted individually or as a Bundle.

3. Defense Against Transaction Reconstruction and Replacement

This mechanism provides a defensive layer against scenarios where an attacker reconstructs a valid transaction and creates another version of it.

Even if the reconstructed version is structurally acceptable, the attacker cannot simply submit it through a different path or node to get it ahead of the original transaction. This is because ATHENA will not issue a new permit for the source account until the required processing state of the previous transaction has been established.

Thus, submission time or submission path cannot bypass the sequential relationship established at the Admission Layer.

4. Benefits of Sequential Transaction Processing

- Transparency and Predictability: The sequential relationship of transactions from the same account is clearly defined, making network behavior more predictable for users.
- Reduced Race Conditions: Consecutive transactions from the same account cannot enter the processing path without respecting the defined order.
- Reduced Transaction Reordering: A subsequent transaction cannot overtake a previous one simply by modifying the fee, path, or submission time.
- Enhanced State Integrity: A defined processing order helps prevent inconsistent states and certain Double-Spend scenarios.
- Easier Auditing: The sequential relationship of requests and their processing results can be reconstructed and verified.

5. Relationship with Conflict Management

Sequential Transaction Processing does not replace Conflict Management.

Conflict Management is used to handle conflicts that arise during the processing phase, while Sequential Transaction Processing aims to prevent some of these conflicts from occurring in the first place—specifically those caused by improper order of transactions from the same account—at the Admission Layer.

6. Foundational Principle

Execution Permit issuance MUST respect the protocol-defined processing order of requests originating from the same account. A subsequent transaction or bundle MUST NOT become eligible for admission before the required processing state of its predecessor has been established according to Host Protocol policy.

This principle ensures that the order of transactions from the same account cannot be bypassed simply by creating a new transaction, modifying the fee, changing the submission path, or reconstructing a previous transaction.

### ATHENA Architecture Diagram

In the ATHENA architecture, the transaction lifecycle begins before the transaction enters the network. By receiving the Admission Request, analyzing the initial transaction information, evaluating the real-time network state, and applying Host Protocol policies, ATHENA determines the complete validation and execution path of the transaction before it enters the network. The result of this process is issued as an Execution Permit, which not only authorizes the transaction to enter the network but also defines its complete execution blueprint. From this point onward, all network components are required to process the transaction without making any independent decisions, strictly following the instructions recorded in the Execution Permit and the policies defined by the Host Protocol.

The transaction lifecycle in the ATHENA architecture proceeds as follows:

1. Transaction Preparation in the Wallet

The user enters the required transaction information into the wallet and reaches the confirmation screen.

2. Admission Request Submission

Before the user is allowed to sign the transaction, the wallet sends an Admission Request containing the information required by the Host Protocol to ATHENA.

3. Analysis and Decision-Making by ATHENA

ATHENA, by analyzing the request information, the current network state, and Host Protocol policies, determines the following:

- Dynamic selection of initial validator nodes
- Formation of initial validation groups through dynamic node selection, resulting in the creation of parallel initial validation pipelines
- Determination of the execution domain
- Selection of the least-loaded execution engine from among the parallel engines within that domain
- Determination of the minimum validation difficulty level
- Registration of the Expected Behavior and Outcome
- Issuance of the Execution Permit
- Storage of the Canonical Copy of the permit

4. Receipt of Permit and Activation of Transaction Signing

After the Execution Permit is issued, it is sent to the wallet, and only upon its receipt is the user enabled to sign the transaction.

5. Transaction Entry into the Network

After the user signs the transaction, the wallet sends the signed transaction together with the Execution Permit directly to the designated initial validator nodes. The transaction never enters any public transaction queue (mempool).

6. Execution Permit Verification and Initial Validation

The initial validator nodes first verify the Execution Permit against the Canonical Copy stored in ATHENA. After the permit is confirmed, initial validation of the transaction is performed according to Host Protocol rules.

7. Routing to the Execution Domain and Engine

After successful completion of the initial validation, the transaction is routed according to the Execution Permit instructions to the designated execution domain, and from among the parallel execution engines within that domain, it is delivered precisely to the execution engine specified in the permit.

8. Transaction Execution

The designated execution engine executes the transaction according to Host Protocol rules. All state transitions, smart contract executions, and other native network logic are performed at this stage.

9. Consensus and Final Recording

After execution is complete, the transaction proceeds through the native consensus mechanism of the Host Protocol. Upon reaching Finality, the transaction is recorded in the global ledger together with the Execution Permit, enabling future verification, auditing, and complete reconstruction of the transaction lifecycle or its validation history.

10. Expected Behavior or Outcome Monitoring

In the final stage, ATHENA compares the recorded outcome with the Expected Behavior or Outcome that was defined at the time of Execution Permit issuance. If any discrepancy is observed, ATHENA prepares and sends an analytical report according to Host Protocol policies. The Host Protocol, using this feedback, can review and optimize its policies to reduce the likelihood of similar conflicts and exceptions recurring in the future.

 ATHENA Architecture Diagram


```
                     ┌────────────────────────┐
                     │         User           │
                     └────────────┬───────────┘
                                  │
                                  │ Enter Transaction Details
                                  ▼
                     ┌────────────────────────┐
                     │        Wallet          │
                     │ Confirmation Screen    │
                     └────────────┬───────────┘
                                  │
                                  │ 1. Admission Request
                                  ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                               ATHENA                                        │
│                 Transaction Lifecycle Management Layer                       │
│                                                                             │
│ • Network Analysis                                                          │
│ • Host Protocol Policy Evaluation                                           │
│ • Dynamic Validator Selection                                               │
│ • Validation Pipeline Formation                                             │
│ • Execution Domain Selection                                                │
│ • Least-loaded Parallel Engine Selection                                    │
│ • Expected Behavior Registration                                            │
│ • Execution Permit Generation                                               │
│ • Canonical Copy Storage                                                    │
└───────────────────────────────┬─────────────────────────────────────────────┘
                                │
                                │ 2. Execution Permit
                                ▼
                     ┌────────────────────────┐
                     │        Wallet          │
                     │ Enable User Signature  │
                     └────────────┬───────────┘
                                  │
                                  │ User Signature
                                  ▼
                     ┌────────────────────────┐
                     │        Wallet          │
                     └────────────┬───────────┘
                                  │
                                  │ 3. Signed Transaction
                                  │    + Execution Permit
                                  ▼
              ┌──────────────────────────────────────┐
              │ Initial Validation Nodes             │
              │ • Permit Verification                │
              │ • Initial Validation                 │
              └────────────────┬─────────────────────┘
                               │
                               │ Forward According
                               │ To Execution Permit
                               ▼
              ┌──────────────────────────────────────┐
              │ Execution Domain                     │
              │ Selected Parallel Execution Engine   │
              │        (Least Loaded)                │
              └────────────────┬─────────────────────┘
                               │
                               │ Execute Transaction
                               ▼
                     ┌────────────────────────┐
                     │ Host Protocol          │
                     │ Native Consensus       │
                     └────────────┬───────────┘
                                  │
                                  ▼
      ┌───────────────────────────────────────────────────────────────┐
      │                  Unified Global Ledger                        │
      │                                                               │
      │ • Transaction                                                  │
      │ • Execution Permit (Must be recorded)                         │
      └───────────────────┬───────────────────────────────────────────┘
                          │
                          │ Expected Behavior Monitoring
                          ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                               ATHENA                                        │
│                                                                             │
│ • Compare Expected vs Actual Result                                         │
│ • Detect Exceptions                                                         │
│ • Analytical Report                                                         │
│ • Feedback to Host Protocol                                                 │
└─────────────────────────────────────────────────────────────────────────────┘
```


### Expected Behavior and Outcome Tracking

One of the key capabilities of the ATHENA architecture is the introduction of the concept of Expected Behavior for each transaction. This concept transforms the transaction lifecycle from a simple "send and wait for result" process into a fully verifiable cycle encompassing planning, execution, monitoring, and result validation.

Expected Behavior refers to the set of outcomes that, based on the information contained in the Admission Request, the rules of the Host Protocol, and the data recorded within the Execution Permit, are anticipated to be observed upon the transaction's finality in the global ledger.

For example, if a wallet requests to transfer 10 TRX from account A to account B, the Expected Behavior of this transaction would include:

- 10 TRX being deducted from account A's balance;
- 10 TRX being added to account B's balance;
- The transaction having been processed exactly according to the validation and execution path specified in the Execution Permit;
- The final result conforming to the rules of the Host Protocol.

For simple transactions, this behavior is usually highly predictable. Conversely, for more complex transactions—such as smart contract calls—the Expected Behavior may involve a set of state changes, outputs, or conditions defined by the contract itself.

For this reason, ATHENA does not attempt to replace the logic of smart contracts; rather, it receives the necessary information to define Expected Behavior from the Host Protocol and incorporates this into the Execution Permit issuance process.

Monitoring Expected Behavior

As described in the ATHENA architecture, ATHENA's responsibility does not end with the issuance of the Execution Permit. ATHENA monitors the lifecycle of each transaction until its final recording in the global ledger. After a transaction reaches Finality, ATHENA compares the recorded outcome with the Expected Behavior.

- If the observed outcome is consistent with the Expected Behavior, the transaction's lifecycle is considered complete.
- However, if the recorded result deviates from the Expected Behavior, ATHENA registers this as an Exception and sends the necessary report to the Host Protocol.

Investigating the cause of this deviation, determining its origin, and deciding on any subsequent actions remain entirely under the authority of the Host Protocol. ATHENA does not modify any consensus, security, or governance rules.

Impact on Resource Allocation

One benefit of this model is that ATHENA can consider the certainty of the Expected Behavior when issuing the Execution Permit. In general:

- Transactions whose Expected Behavior is simple, deterministic, and highly predictable can be scheduled with the minimum processing resources required by the Host Protocol.
- Transactions whose Expected Behavior is more complex, more sensitive, or dependent on shared network state can be directed, according to Host Protocol policies, to stronger validation paths or allocated more resources.

These decisions are fully governed by the Host Protocol's rules; ATHENA merely implements them through the Execution Permit.

Assisting in Detecting Anomalous Behavior

Monitoring Expected Behavior can serve as an effective tool for detecting anomalous behavior within the network.

If the final result recorded in the ledger deviates from the Expected Behavior, the Host Protocol may consider this event as an indicator for investigating issues such as:

- Abnormal validator behavior;
- Potential presence of a malicious Full Node;
- Execution errors;
- Synchronization issues;
- Other exceptional conditions.

ATHENA only identifies and reports the deviation and makes no independent decisions regarding node maliciousness or the imposition of penalties.

Re-validation Capability

If, after reviewing ATHENA's report, the Host Protocol determines that the result of a transaction is unreliable, it can, according to its own policies, decide to re-process the transaction.

In such a case, ATHENA can issue a new Execution Permit for the same request and select a different validation path.

Comparing the results from the independent execution of a transaction across different paths can provide the Host Protocol with valuable data to analyze the root cause of the discrepancy, verify the transaction's execution, and detect anomalous behavior.

Summary

The concept of Expected Behavior is one of the complementary capabilities of the ATHENA architecture for enhancing the Observability and Auditability of the transaction execution process.

This approach is being employed for the first time in a major network, enabling end-to-end monitoring of the transaction lifecycle from the moment an Admission Request is sent to its final recording in the global ledger. It significantly increases the network's transparency, auditability, and performance analysis capabilities.

In this model, without intervening in consensus, ATHENA uses the information from the Admission Request, the Host Protocol rules, and the Execution Permit to compare the final outcome of a transaction against the Expected Behavior. If any discrepancy is observed, it is reported to the Host Protocol.

This approach not only enables full monitoring of the transaction lifecycle but also provides a valuable tool for error analysis, policy improvement, increased validation transparency, and facilitating the investigation of anomalous behavior. Consequently, anomalous behavior can be detected much faster than in conventional models and examined according to Host Protocol policies, without introducing any changes to the blockchain's consensus mechanism or security model.


### Execution Permit–Based Transaction Admission
Eliminating the Public Transaction Waiting Layer


Transaction Admission in Conventional Blockchain Architectures

In conventional blockchain architectures, regardless of the consensus algorithm employed, transaction admission generally follows a common architectural pattern.

After a wallet signs a transaction, the signed transaction is immediately propagated throughout the network and placed into a shared public waiting layer, commonly referred to as the  mempool  or  transaction queue.

This waiting layer temporarily stores incoming transactions until validators or block producers select them for execution.

Consequently, transaction admission and transaction execution are decoupled.

Transactions first become publicly visible to the network, and only afterwards compete for execution resources according to the current processing capacity of the blockchain.


```

Conventional Architecture



      Wallet

         │

         │ Sign Transaction

         ▼

 ┌───────────────────────┐

 │ Public Waiting Layer  │

 │ (Mempool / Queue)     │

 └───────────────────────┘

         │

         ▼

     Validators

         │

         ▼

      Consensus

         │

         ▼

    Global Ledger

```


This architectural model introduces several inherent characteristics:

. Signed transactions enter the network before execution resources are allocated.
. All transactions compete within the same public waiting layer.
. During periods of congestion, the waiting layer naturally grows.
. The execution path of a transaction is unknown until validators eventually select it.
. Every network participant can observe the signed transaction while it waits.
. The public waiting layer therefore becomes an architectural component rather than merely an implementation detail.


Transaction Admission in ATHENA

ATHENA fundamentally redesigns transaction admission.

Instead of allowing a signed transaction to enter the network immediately, the wallet first requests permission to execute the transaction.

This request, referred to as an  Admission Request,  contains only the information required by the Host Protocol for admission decision-making.

No signed transaction exists at this stage.

After receiving the Admission Request, ATHENA evaluates the current operational state of the network together with the policies defined by the Host Protocol and generates an  Execution Permit.

The Execution Permit completely defines the transaction lifecycle before the signed transaction is created.

Depending on Host Protocol policy, the permit may specify:

- validation path;
- initial validator chain;
- execution domain;
- execution engine;
- scheduling policy;
- execution constraints;
- conflict-management policy;
- expected behavior;
- validator quorum;
- and any additional execution parameters required by the Host Protocol.

Only after receiving this permit does the wallet digitally sign the transaction.

The signed transaction is then transmitted  directly  to the validator chain specified inside the Execution Permit.

No public transaction waiting layer exists between the wallet and the designated validators.


```

ATHENA Architecture



      Wallet

         │

         │ Admission Request

         ▼

 ┌────────────────────┐

 │      ATHENA        │

 │ Admission Layer    │

 └────────────────────┘

         │

         │ Execution Permit

         ▼

      Wallet

         │

         │ Sign Transaction

         ▼

 Designated Validator Chain

         │

         ▼

 Native Consensus

         │

         ▼

  Global Ledger

```


Unlike conventional architectures, transaction admission in ATHENA is no longer based on placing signed transactions into a shared waiting pool.

Instead, each transaction receives its execution path before entering the blockchain.

From the moment an Execution Permit is issued, the wallet already knows:

- where the transaction must be sent;
- how it will be validated;
- which execution policies apply;
- and which validators are responsible for processing it.

The transaction therefore follows its predefined execution path immediately after being signed.


Architectural Consequences

This architectural redesign introduces several important properties.

1. Elimination of the Public Waiting Layer

ATHENA removes the public transaction waiting layer from the transaction lifecycle.

Transactions no longer wait inside a shared pool before execution.

Execution resources are allocated first; transaction propagation occurs afterwards.

2. Execution Path Determined Before Transaction Creation

Unlike conventional architectures, ATHENA determines the execution path before the signed transaction is even created.

The wallet receives the complete execution instructions in advance through the Execution Permit.

3. Managed Transaction Admission

ATHENA transforms transaction admission from an uncontrolled broadcast model into a managed admission model.

Instead of allowing unlimited signed transactions to enter the network simultaneously, admission is coordinated according to the real processing capacity defined by the Host Protocol.

4. No Global Competition Between Transactions

Transactions no longer compete inside a common waiting layer.

Each transaction follows only the execution path assigned by its own Execution Permit.

5. Elimination of Unnecessary Public Disclosure

Because signed transactions are not propagated before execution resources have already been assigned, unnecessary public disclosure of transaction information is eliminated.

The signed transaction becomes visible only to the validator chain responsible for processing that specific transaction.


Architectural Security Implications

The elimination of the public waiting layer produces important architectural security consequences.

In conventional blockchain systems, the public mempool represents an observation layer where signed transactions remain publicly accessible before execution.

Researchers have discussed various attack scenarios that rely on observing transactions during this waiting period, including front-running, transaction-copying attacks, denial-of-service amplification, and long-term concerns regarding quantum-assisted cryptanalysis of publicly exposed signatures.

ATHENA removes the architectural condition required for such attacks.

Because signed transactions are never placed into a publicly accessible waiting layer:

- there is no public transaction pool to observe;
- there is no global transaction queue to monitor;
- there is no architectural waiting period between public propagation and execution.

Instead, transactions are signed only after execution authorization has already been granted and are delivered directly to the validator chain designated by the Execution Permit.

Consequently, the public observation surface created by conventional mempool architectures no longer exists within ATHENA.

This should not be interpreted as ATHENA replacing cryptographic security.

Rather, ATHENA removes an entire architectural exposure layer while preserving the native consensus, execution engine, and security model of the Host Protocol.


Native Compatibility

Although ATHENA fundamentally redesigns transaction admission, it leaves the blockchain's native execution model completely unchanged.

Consensus, block production, state transition, validator governance, and finality remain entirely under the authority of the Host Protocol.

ATHENA modifies only the admission architecture—not the blockchain itself.


Architectural Summary

ATHENA replaces public transaction broadcasting with permission-based transaction admission.

Transactions no longer wait inside a shared public pool; instead, each transaction receives its execution path before it is signed, allowing it to move directly from the wallet to its designated validator chain.

By eliminating the public transaction waiting layer as an architectural component, ATHENA removes an entire class of exposure inherent to conventional mempool-based designs while remaining fully compatible with the Host Protocol's native consensus and execution model.


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


### Conflict Prediction and Mitigation Before Transaction Entry

One of ATHENA's core innovations is proactive conflict management.

In conventional architectures, conflicts are typically detected after the transaction has been broadcast to the network and during its execution.

In contrast, ATHENA attempts to predict the likelihood of conflicts before issuing the Execution Permit and before the transaction enters the network—by analyzing the current state of the network and leveraging insights from previously recorded conflicts to select the most appropriate validation and execution path.

Reports generated from actual conflicts are also sent to the Host Protocol, enabling improvements to admission policies, scheduling, node selection, domain selection, and execution engine selection, thereby reducing the likelihood of similar conflicts recurring in the future.

To the best of this research, such an approach—predicting and managing conflicts before the transaction enters the network and before the execution permit is issued—has not been reported in any known blockchain architecture and is one of ATHENA's primary innovations.


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

### Batch Execution Permit — Optional

ATHENA supports Batch Execution Permit functionality.

This capability allows a source account, after receiving a valid batch permit, to submit a set of transactions as a single Bundle to the network.

In this model, the entire Bundle is considered a protocol-level unit with proper authorization and cryptographic integrity, and can be submitted with a single signature applied to the entire content of the Bundle.

A single signature here does not mean reusing a regular signature for multiple independent transactions. Rather, ATHENA defines a new protocol structure in which the entire Bundle is treated as a single Payload for signing.

As a result, any modification to the signed content—including transaction details, amount, destination, or operation type—will invalidate the Bundle's signature.

The primary purpose of the Batch Execution Permit is to support accounts that need to send a large number of transactions.

This capability is particularly suitable for:

- Cryptocurrency exchanges
- Payment platforms
- Distribution services
- High-volume payment systems
- Professional users

The goal is to reduce permit issuance overhead, reduce the number of messages required at the Admission Layer, and enable sending a large number of transactions as a single Bundle.


Submitting a Batch Request

Instead of sending multiple individual permit requests, a source account can submit a single batch request containing n transactions to ATHENA.

All transactions in a batch request must share the same source account.

A source account may have only one active Batch Execution Permit at a time. Until the associated Bundle is finalized, the source account cannot submit a new batch request.

A batch request may include the following information:

- Source account identifier
- List of transactions
- Recipient of each transaction
- Amount of each transaction
- Asset type
- Operation type
- Smart contract parameters, if applicable
- Any other information required by Host Protocol policies


Transaction Review and Path Assignment

Upon receiving a batch request, ATHENA reviews the transactions according to Host Protocol policies.

ATHENA may determine the validation path and processing requirements for each transaction independently.

Therefore, transactions within a Bundle do not necessarily share the same validation or execution path.

The path for each transaction is determined based on the transaction type and Host Protocol policies, and is authorized by ATHENA.

The core requirement for forming a Bundle is that all transactions share the same source account. Other transaction characteristics may differ, provided that Host Protocol permits the combination.


Batch Execution Permit Issuance

After reviewing the batch request, ATHENA issues a Batch Execution Permit.

This permit may include:

- Batch permit identifier
- Bundle identifier
- List of transactions
- Assigned validation path for each transaction
- Initial validator nodes
- Execution domain
- Execution engine or domain assigned for the Bundle
- Permit validity period
- Information regarding reserved resources or balance
- Other details according to Host Protocol policies

Upon issuance, one copy of the Batch Execution Permit is sent to the wallet, and another copy is stored in the Canonical Copy so that the relevant nodes can verify the authenticity and content of the permit.


Bundle Formation and Signing

After receiving the Batch Execution Permit, the source account forms the authorized transactions into a Bundle.

A single signature is then applied to the entire content of the Bundle and the associated permit information.

Once signed, the Bundle is submitted along with the Batch Execution Permit to the designated validation paths.

Since the entire Bundle content is covered by a single signature, any modification to the committed content will break the cryptographic integrity of the Bundle.


Bundle Processing

The wallet prepares the Bundle containing multiple transactions, signs it with a single signature, and submits it together with the permit to the initial validator nodes specified in the Batch Execution Permit.

The designated nodes first verify the Batch Execution Permit and the Bundle signature.

After the permit and signature are confirmed valid, the transactions inside the Bundle are processed and executed according to Host Protocol rules.

Each transaction may have an independent result:

- Success: State changes related to the transaction are applied.
- Failed Execution: State changes related to the failed operation are not applied, but the Failed result is recorded as a processing outcome.

Therefore, the failure of a single transaction does not mean the failure of the entire Bundle.


Bundle Finalization

Once all transactions within the Bundle have reached a determined processing result, the Bundle is considered Finalized as a single processing unit.

In this state:

- No transaction within the Bundle remains in an undetermined processing state.
- The result of each transaction is independently determined.
- Successful transactions have their State Changes applied.
- Failed transactions do not apply any State Changes for the failed operation.
- The result of each transaction is visible and verifiable for accounting, reporting, and auditing purposes.

Therefore:

Bundle Finalization ≠ All Transactions Successful

Bundle Finalization = All Transactions Have a Determined Final Result


Distinction Between Invalid and Failed Execution

To avoid ambiguity, ATHENA distinguishes between two states:

Invalid Transaction:
A transaction that fails initial admission or validation stages—for example, due to invalid structure, incomplete data, incorrect address, or other issues defined by Host Protocol policies—is identified as an Invalid Transaction.

- If the Bundle itself is identified as Invalid: The entire Bundle is rejected.
- If one or more transactions within the Bundle are identified as Invalid: The Bundle continues its validation path without those transactions.

A report of the Invalid Transaction is sent to the Host Protocol, and the source account is notified.

Failed Execution:
Failed Execution transactions within a Bundle have passed the initial admission stages and entered the processing pipeline, but their execution has completed with a Failed result according to Host Protocol rules.

FBT focuses on the second state—preventing the rejection of an entire Bundle due to one or more Failed Execution transactions.


Fee for Failed Transactions

A transaction that has passed the initial admission stages and entered the processing pipeline has consumed computational and network resources.

Therefore, the Host Protocol may define how fees for such transactions are calculated and collected.

A Failed Execution result does not mean State Changes are applied, but the resources consumed during processing may be subject to fees. These fees are deducted from the source account's balance (similar to Ethereum's approach for failed transactions).


Recording Transaction Results

The result of each transaction within a Bundle must be visible and verifiable.

If a transaction fails after entering the processing pipeline, its Failed result is recorded as part of the final Bundle outcome.

Recording a Failed result does not mean State Changes are applied. It indicates that the transaction was valid, entered the processing pipeline, and completed with a Failed execution result.

This information can be used for accounting, reporting, auditing, and Bundle status review.


Relationship Between Batch Execution Permit and FBT

The Batch Execution Permit and Finalized Bundle Transactions (FBT) are related but distinct concepts:

- Batch Execution Permit: The mechanism for batch authorization and admission.
- FBT: The mechanism for complete Bundle finalization.

The overall flow is as follows:

```
Account → Batch Admission Request → ATHENA → Batch Execution Permit → Signed Bundle → Validation & Execution → Individual Results → Bundle Finalization
```

In this model, ATHENA is responsible for issuing the permit and determining the admission path, while the Host Protocol defines the validation rules, transaction execution, resource calculation, and final result determination.


Foundational Principle

A Batch Execution Permit MUST be cryptographically bound to all transactions contained within its associated Bundle.

A valid Bundle MAY contain transactions with different execution outcomes.

An Invalid Transaction MUST NOT prevent the Bundle from being processed, provided the Bundle itself remains valid.

The final Bundle result MUST include an independently verifiable outcome for each transaction contained within the Bundle.

In this way, the Batch Execution Permit enables batch transaction submission while maintaining security, transparency, and complete finalization.
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

After the Execution Permit is issued, one copy is sent to the requesting wallet, and the reference copy is retained in the Provisional State, so that the relevant components can verify the authenticity and conformity of the received permit.

After receiving the Execution Permit, the wallet enables the user to sign the transaction and, after signing, sends the transaction along with the permit to the designated initial validation nodes.

### Phase 4: Transaction Signing After Receiving the Execution Permit

With network support of the AVP-DS capability, the user is authorized to sign the transaction only when the wallet has sent the information required for issuing the Execution Permit to the Network Protocol and has received the Execution Permit.

Therefore, after receiving the permit, the wallet enables the user to sign the transaction and sends the transaction, along with the Execution Permit, to the initial validation nodes specified in the Execution Permit.

### Phase 5: Direct Submission of the Transaction to the Initial Validation Nodes

First, based on the Network Protocol's instructions, the wallet prepares the transaction submission request along with the required information and sends it to the Network Protocol for evaluation.

After receiving the Execution Permit from the Network Protocol, the wallet enables the user to sign the transaction. After the user signs the transaction, the wallet sends it, along with the Execution Permit, directly to the initial validation nodes designated in that same permit.

In this manner, the signed transaction does not enter any public transaction queue or public waiting layer and will enter the validation process via the dedicated path determined in the Execution Permit.

### Phase 6: Full Verification of the Execution Permit

Before validation begins, the initial validation nodes are required to verify the full contents of the Execution Permit against the reference copy retained in the Provisional State, fully and line by line, within the framework of the Network Protocol.

This verification covers all components of the permit. In the event of any discrepancy, the transaction is rejected and the relevant report is sent to the Network Protocol.

Upon successful verification and confirmation of the Execution Permit and its full conformity with the Provisional State — given that the complete roadmap of addressing, routing, and the components responsible for validation has been fully determined and specified in the Execution Permit — all relevant and designated components are required to follow exactly the instructions recorded in that same permit, without independent decision-making regarding the path or assigned duties.

### Phase 7: Initial Validation

The initial validation nodes designated on a per-transaction basis, in accordance with the Execution Permit issued by the Network Protocol, after receiving the transaction along with the Execution Permit and after completing full and line-by-line verification against the copy stored in the Canonical Copy, perform preliminary checks based on the items specified by the Network Protocol — including the following:

- Digital signature validity
- Transaction structure
- Account balance
- Request validity
- Any other checks defined by the Network Protocol

After successful completion of initial validation, the designated nodes send the transaction to the specified execution domain and, from among the set of parallel execution engines in that domain, to the exact execution engine specified in the Execution Permit.

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

The execution components designated in the Execution Permit, upon identifying a conflict or exceptional condition, review the Execution Permit and the completed validation stages, and send the verification report and conflict information to the Network Protocol. Decision-making regarding continuing the process, re-execution, issuing a new permit, changing the path, or rejecting the transaction rests exclusively with the Network Protocol, and all relevant components are required to execute its instructions.

Analytical Report and Prevention of Conflict Recurrence

For each identified conflict, the Network Protocol prepares and maintains an analytical report containing the cause, the manner of identification, the actions taken, and the final outcome. This information is used to improve the policies for issuing Execution Permits, selecting the validation path, validation nodes, domain, and execution engine, and to prevent the recurrence of similar conflicts in future transactions.

### Phase 12: Consensus and Finality

The AVP-DS capability is not designed to change or replace the network's fundamental mechanisms, including consensus layers, protocol policies, or core validation rules.

Through the separation of the Decision Layer from the Execution Layer, this capability enables the dynamic use of new capacities, increases validation capacity through parallel paths, manages the transaction from the request stage in the wallet to registration in the ledger, and prevents conflicts before the transaction enters the network.

Throughout all these stages, the Network Protocol remains the exclusive decision-making authority, and the components relevant to each transaction follow the instructions issued in the Execution Permit. Therefore, supporting networks can utilize their resources and capacities in a coordinated, dynamic, intelligent, and scalable manner, without requiring changes to the fundamental mechanisms, consensus, or core rules of the network.

### Phase 13: Registration in the Network Ledger (Transaction Information Alongside the Execution Permit)

In many conventional architectures, when a transaction is registered in the network ledger, only items such as the final transaction result, the signature hash, the sender and receiver addresses, the amount and type of asset, and other public information are visible — and no information about the validation path and relevant components, including the responsible nodes or the execution engine, is present.

In contrast, with network support of the AVP-DS capability, it becomes possible to fully reconstruct the validation path, in addition to the public information. This transparency — the ability to reconstruct and audit — is among the benefits of network support of AVP-DS.

For this reason, the network must store the Execution Permit or the verifiable cryptographic commitment associated with the transaction, along with the other public transaction information, in the network ledger.

This information enables independent auditing, reconstruction of the transaction's execution path, verification of the performance of network components and monitoring of the behavior of the relevant components (including nodes and engines), evaluation of validator performance, and analysis of the validation process — even years after finality.
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
