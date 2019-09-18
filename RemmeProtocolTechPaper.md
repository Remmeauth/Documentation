# Remme Protocol Technical paper

**Abstract:** The Remme Protocol software introduces a blockchain architecture designed to enable vertical and horizontal scaling of decentralized applications. This is achieved by creating an operating system-like construct upon which applications can be built. The software provides accounts, authentication, databases, asynchronous communication, and the scheduling of applications across many CPU cores or clusters. The resulting technology is a blockchain architecture that may ultimately scale to millions of transactions per second, eliminates user fees, and allows for quick and easy deployment and maintenance of decentralized applications, in the context of a governed blockchain.

**PLEASE NOTE: CRYPTOGRAPHIC TOKENS CITED IN THIS PAPER REFER TO CRYPTOGRAPHIC TOKENS ON A LAUNCHED BLOCKCHAIN THAT ADOPTS THE REMME PROTOCOL SOFTWARE. THEY DO NOT REFER TO THE ERC-20 COMPATIBLE TOKENS BEING DISTRIBUTED ON THE ETHEREUM BLOCKCHAIN IN CONNECTION WITH THE REMME TOKEN DISTRIBUTION.**

**DISCLAIMER:** This Remme Protocol Technical Paper is for information purposes only. Remme Protocol does not guarantee the accuracy of nor the conclusions reached in this paper, and this paper is provided “as is”. Remme Protocol does not make and expressly disclaims all representations and warranties, express, implied, statutory or otherwise, whatsoever, including, but not limited to: (i) warranties of merchantability, fitness for a particular purpose, suitability, usage, title or noninfringement; (ii) that the contents of this paper are free from error; and (iii) that such contents will not infringe third-party rights. Remme Protocol and its affiliates shall have no liability for damages of any kind arising out of the use, reference to, or reliance on this paper or any of the content contained herein, even if advised of the possibility of such damages. In no event will Remme Protocol or its affiliates be liable to any person or entity for any damages, losses, liabilities, costs or expenses of any kind, whether direct or indirect, consequential, compensatory, incidental, actual, exemplary, punitive or special for the use of, reference to, or reliance on this paper or any of the content contained herein, including, without limitation, any loss of business, revenues, profits, data, use, goodwill or other intangible losses.

# Background

Remme Protocol utilizes blockchain technology to replace traditional centralized instances of Public Key Infrastructure with a blockchain-based Network of Trust.

Choosing the right platform to start with is essential for every blockchain project. It’s imperative that businesses operating in the industry select a blockchain whose multifunctionality, adaptability, scalability, security and community support match their requirements.

After thorough consideration, we have settled upon the EOSIO codebase as being the ideal fit for the Remme Protocol software to start building on.

The EOSIO codebase is currently powering the EOS ecosystem, which is among the top known cryptocurrencies. As a consequence, it has been adversarially tested at a very high level and has significant industry recognition.

Designed to scale, EOSIO is capable of processing thousands of transactions per second and offers free rate limited transactions, low latency block confirmation (0.5 seconds), low-overhead Byzantine Fault Tolerant finality, hierarchical role-based permissions, and focus on Inter Blockchain Communication. These are the reasons the Remme Protocol software will be built on top of EOSIO. This paper describes the features inherited from EOSIO and those brought by Remme Protocol.

# Requirements for Blockchain Applications

In order to gain widespread use, applications on the blockchain require a platform that is flexible enough to meet the following requirements:

## Support Millions of Users

Competing with centralized businesses requires blockchain technology capable of handling tens of millions of active daily users. In certain cases, an application may not work unless a critical mass of users is reached and therefore a platform that can handle very large numbers of users is paramount.

## Free Usage

Application developers need the flexibility to offer users free services; users should not have to pay in order to use the platform or benefit from its services. A blockchain platform that is free to use for users will likely gain more widespread adoption. Developers and businesses can then create effective monetization strategies.

## Easy Upgrades and Bug Recovery

Businesses building blockchain-based applications need the flexibility to enhance their applications with new features. The platform must support software and smart contract upgrades.

All non-trivial software is subject to bugs, even with the most rigorous of formal verification. The platform must be robust enough to fix bugs when they inevitably occur.

## Low Latency

A good user experience demands reliable feedback with a delay of no more than a few seconds. Longer delays frustrate users and make applications built on a blockchain less competitive with existing non-blockchain alternatives. The platform should support low latency of transactions.

## Sequential Performance

There are some applications that just cannot be implemented with parallel algorithms due to sequentially dependent steps. Applications such as exchanges need enough sequential performance to handle high volumes. Therefore, the platform should support fast sequential performance.

## Parallel Performance

Large scale applications need to divide the workload across multiple CPUs and computers.

# Consensus Algorithm (BFT-DPOS)

The Remme Protocol software utilizes the only known decentralized consensus algorithm proven capable of meeting the performance requirements of next-gen PKI applications on the blockchain, [Delegated Proof of Stake (DPOS)](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this-missing-white-paper).
Under this algorithm, those who hold a certain amount of tokens on a blockchain adopting the Protocol software may select Block Producers (BPs) through a continuous voting mechanism.
Anyone who accumulates a minimum required amount of tokens may choose to participate in the block producer election by running for top 21 status or vote for other candidates they trust and feel confident about.
Active participation in the network's governance (consistent voting and keeping a minimum required token balance staked) is a requirement to get a status of Guardian and participate in the stake reward distribution process. 
The power of the vote is proportional to the number of tokens that the account has agreed to stake (the more tokens you stake, the more influential your vote).
This system of governance with the block producer election process puts the token holders in charge and sets proper incentives to elect the most credible and professional candidates to produce blocks.
Otherwise, token holders would incur significant financial losses if the candidates they elected misbehaved and the network delivered a poor service to end users.

The Remme Protocol software enables blocks to be produced exactly every 0.5 seconds and exactly one producer is authorized to produce a block at any given point in time. If the block is not produced at the scheduled time, then the block for that time slot is skipped. When one or more blocks are skipped, there is a 0.5 or more second gap in the blockchain.

Using the Remme Protocol software, blocks are produced in rounds of 126 (6 blocks each, times 21 producers). At the start of each round, 21 unique BPs are chosen by the preference of votes cast by token holders. The selected producers are scheduled in an order agreed upon by 15 or more producers.

If a producer misses a block and has not produced any block within the last 24 hours, they are removed from consideration until they notify the blockchain of their intention to start producing blocks again. This ensures the network operates smoothly by minimizing the number of blocks missed by not scheduling producers who are proven to be unreliable.

Under normal conditions a DPOS blockchain does not experience any forks because, rather than compete, the BPs cooperate to produce blocks. In the event of a fork, consensus will automatically switch to the longest chain. This method works because the rate at which blocks are added to a blockchain fork is directly correlated to the percentage of BPs that share the same consensus. In other words, a blockchain fork with more producers on it will grow in length faster than one with fewer producers, because the fork with more producers will experience fewer missed blocks.

Furthermore, no BP should be producing blocks on two forks at the same time. A BP caught doing this will likely be voted out. Cryptographic evidence of such double production may also be used to automatically remove abusers.

Byzantine Fault Tolerance (BFT) is added to traditional DPOS by allowing all producers to sign all blocks so long as no producer signs two blocks with the same timestamp or the same block height. Once 15 producers have signed a block, the block is deemed irreversible.

BFT Delegated Proof of Stake is robust under every conceivable natural network disruption and even secure in the face of the corruption of a large minority of producers. Unlike some competing algorithms, BFT can continue to function when a majority of producers fail. During this process, the community can vote to replace the failed producers until it can resume 100% participation.

## Block Rewards

The block reward is divided into the following proportions:
- 60% - **Stake Reward** - Shared between all Guardians proportionally to their stake.
- 30% - **Vote Reward** - Shared between the Top 25 Block Producers proportionally to the number of votes they received from Guardians and other accounts (1 staked token = 1 vote).
- 10% - Remme Savings account


The block rewards are credited to the account with a call to the system’s contract method claimrewards. Rewards are liquid and may be staked with a separate transaction.

BP does not get rewarded for the missed blocks. The claimrewards method credits rewards in prorated to the number of blocks that got added into the blockchain by a BP. The remainder (rewards for the missed blocks) gets credited to the Remme Savings account.

## How to Become a Guardian

The Guardians play a key role in the protocol's governance process by delegating this responsibility (via voting) to the Block Producers.
In Remme Protocol, there are specific criteria that need to be met by an account to get the Guardian status and participate in stake reward distribution:
- An account needs to stake a minimum 250k REM
- Tokens are locked for the first six months (you cannot change your mind once you stake)
- The power of the vote is built up gradually to 100% over six months on a weekly basis. Note: Guardian earns full and liquid rewards from the start

In order to maintain the Guardian status, each account will have to re-assert their vote every month. With those that do not keep their votes up to date for more than a month:
- Account stops getting stake rewards
- The influence of last recorded vote decays by half every year

In case a Guardian stakes more tokens during the initial locking period, it will increase the locking proportionally.
For example, an account starts with 100M tokens staked with the initial six-month locking period. After 1.5 months they stake an additional 200M tokens. As a result, the locking period is adjusted from the remaining 4.5 months to 5.5 months with a total of 300M tokens staked. 6mon - 6mon*(100M*1.5/6)/(100M+200M) = 5.5mon.

Guardians do not need to operate a full node. Staking, voting and claiming rewards can be done via a light client.

## How to become a Block Producer

Any account can register as Block Producer by calling the **regproducer** action in the system contract. It is expected, that BPs would specify the website as a parameter and this website would contain a bp.json file in the root folder. The bp.json has to be compatible with the standard [described here](https://github.com/eosrio/bp-info-standard). 

## Block Producer Elections

There are different groups of Block Producers depending on the number of votes they received from Guardians and other accounts:
- The Top 20: Active BPs responsible for producing and continuously adding new blocks to the blockchain.
- The Top 21-25: BPs become Active to produce blocks in shifts and rotate every six hours. (There is always maximum 21 Active BPs at a given moment)
- The rest: Standby BPs not producing blocks at a given moment, but may become Active at some point.

Remme Protocol grants voting responsibility to the accounts that have expressed their long-term engagement via staking REM tokens. Once staked, any account gets the ability to vote (in the proportion of 1 staked token = 1 vote).
Participants should cast their votes in favor of BPs they trust and believe to be the best candidates to produce blocks responsibly. It is expected that BPs will cast their available votes in their own favor.

Some notes:
- It is permissible to change the candidates account votes for and, in this way, immediately vote out the BPs that happen to deliver poor service to the network.
- It is also possible to vote for multiple candidates simultaneously, however, the number of votes they receive would be split equally among the candidates and would total the size of the staked tokens by the BP.

## Unstaking Tokens

An account may decide to unstake tokens (not permitted during the lock period over the first six months of staking). After this, staked tokens will gradually start to release over a period of six months on a weekly basis. This is done to secure the network from speculative behavior among Guardians and BPs.

For example, an account with 300M staked tokens starts to unstake. After 2 months they decide to stake tokens again. There were 200M tokens left pending release so those tokens come back into the staked and unlocked state. If the account decides to additionally stake the tokens that were previously released, the entire stake would get locked again per the locking formula described earlier.

# Accounts

The Remme Protocol software permits all accounts to be referenced by a unique human-readable name of up to 12 characters in length. The name is chosen by the creator of the account.

In a decentralized context, application developers will pay the nominal cost of account creation to sign up a new user. Traditional businesses already spend significant sums of money per customer they acquire in the form of advertising, free services, etc. The cost of funding a new blockchain account should be insignificant in comparison. Fortunately, there is no need to create accounts for users already signed up by another application.

## Actions & Handlers

Each account can send structured Actions to other accounts and may define scripts to handle Actions when they are received. The Remme Protocol software gives each account its own private database which can only be accessed by its own action handlers. Action handling scripts can also send Actions to other accounts. The combination of Actions and automated action handlers is how Remme Protocol defines smart contracts.

To support parallel execution, each account can also define any number of scopes within their database. The BPs will schedule transactions in such a way that there is no conflict over memory access to scopes and therefore they can be executed in parallel.

## Role-Based Permission Management

Permission management involves determining whether or not an Action is properly authorized. The simplest form of permission management is checking that a transaction has the required signatures, but this implies that required signatures are already known. Generally, authority is bound to individuals or groups of individuals and is often compartmentalized. The Remme Protocol software provides a declarative permission management system that gives accounts fine-grained and high-level control over who can do what and when.

It is critical that authentication and permission management be standardized and separated from the business logic of the application. This enables tools to be developed to manage permissions in a general-purpose manner and also provides significant opportunities for performance optimization.

Every account may be controlled by any weighted combination of other accounts and private keys. This creates a hierarchical authority structure that reflects how permissions are organized in reality and makes multi-user control over accounts easier than ever. Multi-user control is the single biggest contributor to security, and, when managed properly, can greatly reduce the risk of theft due to hacking.

The Remme Protocol software allows accounts to define what combination of keys and/or accounts can send a particular Action type to another account. For example, it is possible to have one key for a user's social media account and another for access to the exchange. It is even possible to give other accounts permission to act on behalf of a user's account without assigning them keys.

### Named Permission Levels

Using the Remme Protocol software, accounts can define named permission levels, each of which can be derived from higher level named permissions. Each named permission level defines an authority; authority is a threshold multi-signature check consisting of keys and/or named permission levels of other accounts. For example, an account's "Friend" permission level can be set for an Action on the account to be controlled equally by any of the account's friends.

### Permission Mapping

The Remme Protocol software allows each account to define a mapping between a contract/action or contract of any other account and their own Named Permission Level. For example, an account holder could map the account holder's social media application to the account holder's "Friend" permission group. With this mapping, any friend could post as the account holder on the account holder's social media. Even though they would post as the account holder, they would still use their own keys to sign the Action. This means it is always possible to identify which friends used the account and in what way.

### Evaluating Permissions

When delivering an Action of type "**Action**", from **@alice** to **@bob** the Remme Protocol software will first check to see if **@alice** has defined a permission mapping for **@bob.groupa.subgroup.Action**. If nothing is found then a mapping for **@bob.groupa.subgroup** then **@bob.groupa**, and lastly **@bob** will be checked. If no further match is found, then the assumed mapping will be to the named permission group **@alice.active**.

Once a mapping is identified then signing authority is validated using the threshold multi-signature process and the authority associated with the named permission. If that fails, then it traverses up to the parent permission and ultimately to the owner permission, **@alice.owner**.

#### Default Permission Groups

The Remme Protocol technology also allows all accounts to have an "owner" group which can do everything and an "active" group which can do everything except change the owner group. All other permission groups are derived from "active".

#### Parallel Evaluation of Permissions

The permission evaluation process is "read-only" and changes to permissions made by transactions do not take effect until the end of a block. This means that all keys and permission evaluation for all transactions can be executed in parallel. Furthermore, this means that a rapid validation of permission is possible without starting costly application logic that would have to be rolled back. Lastly, it means that transaction permissions can be evaluated as pending transactions are received and do not need to be re-evaluated as they are applied.

All things considered, permission verification represents a significant percentage of the computation required to validate transactions. Making this a read-only and trivially parallelizable process enables a dramatic increase in performance.

When replaying the blockchain to regenerate the deterministic state from the log of Actions there is no need to evaluate the permissions again. The fact that a transaction is included in a known good block is sufficient to skip this step. This dramatically reduces the computational load associated with replaying an ever-growing blockchain.

## Actions with Mandatory Delay

Time is a critical component of security. In most cases, it is not possible to know if a private key has been stolen until it has been used. Time-based security is even more critical when people have applications that require keys to be kept on computers connected to the internet for daily use. The Remme Protocol software enables application developers to indicate that certain Actions must wait a minimum period of time after being included in a block before they can be applied. During this time, they can be canceled.

Users can then receive a notice via email or text message when one of these Actions is broadcast. If they did not authorize it, then they can use the account recovery process to recover their account and retract the Action.

The required delay depends upon how sensitive the operation is. Paying for a coffee might have no delay and be irreversible in seconds, while buying a house may require a 72-hour clearing period. Transferring an entire account to new control may take up to 30 days. The exact delays are chosen by application developers and users.

## Recovery from Stolen Keys

The Remme Protocol software provides users a way to restore control of their account when keys are stolen. An account owner can use any owner key that was active in the last 30 days along with approval from their designated account recovery partner to reset the owner key on their account. The account recovery partner cannot reset control of the account without the help of the owner.

There is nothing for the hacker to gain by attempting to go through the recovery process because they already "control" the account. Furthermore, if they did go through the process, the recovery partner would likely demand identification and multi-factor authentication (phone and email). This would likely compromise the hacker or gain the hacker nothing in the process.

This process is also very different from a simple multi-signature arrangement. With a multi-signature transaction, another entity is made a party to every transaction that is executed. By contrast, with the recovery process, the recovery partner is only a party to the recovery process and has no power over the day-to-day transactions. This dramatically reduces costs and legal liabilities for everyone involved.

# Token Model and Resource Usage

All blockchains are resource constrained and require a system to prevent abuse. With a blockchain that uses Remme Protocol software, there are three broad classes of resources that are consumed by applications:

1. Bandwidth and Log Storage (Disk);
2. Computation and Computational Backlog (CPU); and
3. State Storage (RAM).

Bandwidth and computation have two components: instantaneous usage, and long-term usage. A blockchain maintains a log of all Actions and this log is ultimately stored and downloaded by all full nodes. With the log of Actions, it is possible to reconstruct the state of all applications.

The computational debt comprises calculations that must be performed to regenerate state from the Action log. If the computational debt grows too large then it becomes necessary to take snapshots of the blockchain's state and discard the blockchain's history. If computational debt grows too quickly then it may take 6 months to replay 1 year’s worth of transactions. It is critical, therefore, that the computational debt is carefully managed.

Blockchain state storage is information that is accessible from application logic. It includes information such as digital keys, revocation status, and account balances. If the state is never read by the application, then it should not be stored. For example, identity scans and home address are not read by application logic, so they should not be stored in the blockchain's state. Meanwhile, the existence of a document, the number of votes, and other properties do get stored as part of the blockchain's state.

Adopting the Remme Protocol software on a launched blockchain means bandwidth and computational capacity are allocated on a fractional reserve basis because they are transient (unused capacity cannot be saved for future use).

Compared to the EOS blockchain, the Remme Protocol software offers a simplified resource management experience.

Due to the major focus on next-gen PKI use cases, we assume that most of the core services within the network are provided by the BPs based on the system smart contracts and only a smaller part of services by the community dApps on top of the core ones. To address this, Remme Protocol allocates the available supply of all three resources (RAM, CPU, NET) simultaneously and proportionally to the number of tokens in long term staking contract.
For example, by staking 1% of the total token supply, an account gets the potential to utilize 1% of all resources (either by running its own dApp or using someone else's dApp).

On the contrary to the user smart contracts, the system contracts provide various PKI services based on a subscription or per use model.
For example, a user would pay a certain flat fee to store a device public key and its revocation status for a period of one year. After the period ends, the key transits into an expired state and the system contract frees up the RAM resources.

Remme Protocol has a flat fee to create an account. A new account gets created with the minimum required allocation of CPU, NET and RAM resources that allows users to store the account data in the state and perform about 3-5 average transactions per day at no additional cost. The goal is to let the vast majority (up to 95%) of users transact for free (assuming a regular user would not need more than 5 transactions a day).

Removing this hassle of resource management and simplifying the user experience, we believe that a blockchain running on the Protocol will become very friendly and intuitive for newcomers who are not familiar with blockchain technology and its peculiarities. With this approach, we expect most users to access various high-level applications without even noticing the blockchain behind that powers them. We expect most of the users to be onboarded (and sponsored with a new account if needed) by businesses or dApps that benefit from improved security or other next-gen PKI use cases.


## Objective and Subjective Measurements

As discussed earlier, instrumenting computational usage has a significant impact on performance and optimization; therefore, all resource usage constraints are ultimately subjective, and enforcement is done by BPs according to their individual algorithms and estimates. These would typically be implemented by a BP via the writing of a custom plugin.

That said, there are certain things that are trivial to measure objectively. The number of Actions delivered, and the size of the data stored in the internal database are cheap to measure objectively. The Remme Protocol software enables BPs to apply the same algorithm over these objective measures but may choose to apply stricter subjective algorithms over subjective measurements.

## Receiver Pays

Traditionally, it is the business that pays for office space, computational power, and other costs required to run the business. The customer buys specific products from the business and the revenue from those product sales is used to cover the business costs of operation. Similarly, no website obligates its visitors to make micropayments for visiting its website to cover hosting costs. Therefore, decentralized applications should not force their customers to pay the blockchain directly for the use of the blockchain.

A launched blockchain that uses the Remme Protocol software does not require its users to pay the blockchain directly for its use and therefore does not constrain or prevent a business from determining its own monetization strategy for its products.

While it is true that the receiver can pay, Remme Protocol enables the sender to pay for bandwidth, computation, and storage. This empowers application developers to pick the method that is best for their application. In many cases, the sender-pays model significantly reduces complexity for application developers who do not want to implement their own rationing system. Application developers can delegate bandwidth and computation to their users and then let the “sender pays” model enforce the usage. From the perspective of the end user, it is free, but from the perspective of the blockchain, it is the sender-pays model.


## Delegating Capacity

A holder of tokens on a blockchain that has launched adopting the Remme Protocol software, who may not have an immediate need to consume all or part of the available bandwidth, can delegate or rent such unconsumed bandwidth to others; the BPs running the Remme Protocol software on such a blockchain will recognize this delegation of capacity and allocate bandwidth accordingly.

## Separating Transaction Costs from Token Value

One of the major benefits of the Remme Protocol software is that the amount of bandwidth available to an application is entirely independent of any token price. If an application owner holds a relevant number of tokens on a blockchain adopting the Remme Protocol software, then the application can run indefinitely within a fixed state and bandwidth usage. In such a case, developers and users are unaffected by any price volatility in the token market and therefore not reliant on a price feed. In other words, a blockchain that adopts the Remme Protocol software enables BPs to naturally increase bandwidth, computation, and storage available per token independent of the token's value.

A blockchain using the Remme Protocol software also awards BPs with tokens earned by the network every time they produce a block. The value of the tokens will impact the amount of bandwidth, storage, and computation a producer can afford to purchase; this model naturally leverages rising token values to increase network performance.

## State Storage Costs

Storage of the user application state will require an application developer to hold tokens until that state is deleted. If the state is never deleted, then the tokens are effectively removed from circulation.

## Freezing Accounts

Sometimes a smart contract behaves in an aberrant or unpredictable manner and fails to perform as intended; other times an application or account may discover an exploit that enables it to consume an unreasonable amount of resources. When such issues inevitably occur, the BPs have the power to rectify such situations.

The BPs on all blockchains have the power to select which transactions are included in blocks which gives them the ability to freeze accounts. A blockchain using the Remme Protocol software formalizes this authority by subjecting the process of freezing an account to a 15/21 vote of active producers. If producers abuse this power they can be voted out and an account will be unfrozen.

## Changing Account Code

When all else fails and an "unstoppable application" acts in an unpredictable manner, a blockchain using the Remme Protocol software allows the BPs to replace the account's code without hard forking the entire blockchain. Similar to the process of freezing an account, this replacement of the code requires a 15/21 vote of elected BPs.

## User Agreement

The Remme Protocol software enables the establishment of a peer-to-peer terms of service agreement or a binding contract among those users who sign it, referred to as an "agreement". The content of this agreement defines obligations among the users which cannot be entirely enforced by code and facilitates dispute resolution by establishing jurisdiction and choice of law along with other mutually accepted rules. Every transaction broadcast on the network must incorporate the hash of the agreement as part of the signature and thereby explicitly binds the signer to the contract.

The agreement also defines the human readable intent of the Protocol source code. This intent is used to identify the difference between a bug and a feature when errors occur and guides the community on what fixes are proper or improper.

## Upgrading the Protocol

The Remme Protocol software defines the following process by which the Protocol, as defined by the canonical source code, can be updated:

1. BPs propose a change to the code and obtain 15/21 approval.
2. BPs maintain 15/21 approval of the new code for 30 consecutive days.
3. Changes to the code take effect 7 days later, giving all non-producing full nodes 1 week to upgrade after ratification of the source code.
4. All nodes that do not upgrade to the new code shut down automatically.

### Emergency Changes

The BPs may accelerate the process if a software change is required to fix a harmful bug or security exploit that is actively harming users.

# Conclusion

The Remme Protocol software is designed from experience with proven concepts and best practices, and represents fundamental advancements in blockchain technology. The software is part of a holistic blueprint for a globally scalable blockchain society in which decentralized applications can be easily deployed and governed.

# Reference
This Paper is based on the EOS.IO materials.
