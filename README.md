---
lip: <to be assigned>
title: Luck Improvement Proposal
author: vjudeu (@vjudeu)
discussions-to: https://bitcointalk.org/index.php?topic=5254068
status: Draft
type: Informational
created: 2020-11-22
---

This is the first Luck Improvement Proposal (LIP). I hope there will be more LIPs in the future and other people who want to support Luck and help creating a coin that is truly pool-resistant will share their ideas.

## Simple Summary

This proposal is the author's solution to the failed hard fork at block 388,000 in the Luck coin to avoid similar situations in the future.

## Abstract

The author believes that hard forks has many drawbacks and should be avoided if possible. However, the reality is that sometimes nobody has any idea how to solve some problem in other way than hard fork. The main aim of this proposal is to reduce harm caused by hard forks and to make sure that most nodes will switch to the new version and don't try to create a split in the network.

## Motivation

Currently, hard forks are rolled out by developers just by publishing a new version and saying that "everyone have to switch before block number X". This is sufficient when the network is small and consist of just a few nodes. It was true during hard fork at block 39,200, but it turned out that the situation is now different. The hard fork at block 388,000 failed mostly because a lot of nodes just sticked with older version and ignored the new one. In this proposal the author describes what should be done before releasing a new version to minimize that risk in the future.

## Specification

The new version that supports some hard fork should include different extraNonce in all mined blocks. By default it consists of software name, operating system name and software version. This should be left unchanged. 

The new version should be released long before activating new rules.

The new version should not activate some hard fork automatically.

Hard fork activation should be performed in a normal transaction that any non-mining user can create.

Hard fork activation should be done by spending premine coins.

There should also be a transaction that will cancel such fork if included.

After one of such transaction will be included in mined block, the other one should never be mined and treated as double spending attempt if ever broadcasted or mined.

## Rationale

By including different version in extraNonce, it is possible to check how many blocks are produced by miners supporting some hard fork and how many blocks are still refusing to update.

Releasing the new version long before update gives people some time to upgrade. It is better to create one stable version than fifty unstable ones. As the coin is getting more serious and real money are at stake, some precautions are needed to make sure that everything will roll out as expected.

Not switching to the new rules automatically is crucial, because it may turn out that most miners don't want to upgrade and then it will definitely cause a split in the network. Developers should have the right to activate or deactivate hard fork once and miners should have the right to accept new version or reject it.

The author assumes that developers may not have enough mining power to create blocks in the future, and that's why it should be possible to activate hard fork when being non-mining user. To avoid network split, hard fork should be activated only when some specific data will be placed on chain. In this way, when it will turn out that the new version is somehow flawed, it will be possible to fix it, make a new release and keep calm, because previously upgraded nodes won't activate new rules automatically.

To make sure that the fork was activated by developers, spending (or at least signing) premine coins is needed, because they are in developers' hands and it is sufficient to prove that hard fork was activated by them. Such transaction should contain some data indicating that some hard fork was activated, and then all new nodes will switch into new rules just after the block containing such transaction.

Transaction that cancel the fork is needed to make sure that the hard fork will never be activated after some time. In this way, newly released client will observe premine, waiting for two transactions: one that will activate the hard fork and one that will cancel it.

For each hard fork, only one such transaction should be present in the chain: activating the fork or rejecting it. Then, all people will clearly see which fork is activated and which is rejected and never will be turned on.

## Backwards Compatibility

For now, there are two different networks after block 388,000. The author calls them Luck and Luck Classic. Luck is the version for which new rules were activated and Luck Classic represents all nodes that rejected new version and sticked with the old software. As the time of writing, there are over 400,000 blocks in both networks, which means that all blocks after the fork have at least 12,000 confirmations. That amount of work cannot be simply reverted, because it will undermine fundamental rules that makes this network valuable.

Currently used exchange, qTrade, at the time of writing is still using the old version. Buying, selling, depositing and withdrawing coins works under old rules, nobody is stopped from doing that. There is also no way to stop people from On The Chain trading by using Discord or other communication channels.

To fix the whole situation, the only possible solution from author's perspective is making a better version, convincing people to upgrade and activating it only after reaching consensus. Just pushing new versions without checking how many users will upgrade or will it behave correctly in the current network on many different computers is a straight way to dumping this coin value to zero.

## Test Cases

There was a testnet before releasing this coin. All testnet coins were burned before releasing mainnet. Because now the network is splitted and there are many problems with new version's stability, it should be tested before activating on mainnet. Another mistakes will cause more problems, we should test it on real users' machines.

## Implementation

The new version should be aware of the split after block 388,000. It should handle properly both network rules to achieve better stability and give an incentive to upgrade. Now, some people may even run two different versions of the Luck software, they should get the new, better version that can handle both networks properly to avoid more problems with stability.

The new version should signalize the support of new rules activation in both chains. It should be possible to mine two different chains and include the new version in extraNonce in both chains.

The client should switch to the new rules on both network, causing the split to be solved if the new rules will be activated. Blocks mined under new rules (submitted to both networks) should be binary identical to avoid another splits.

The client should observe premine, looking for transaction activating new rules on both chains or transaction rejecting it and leaving the whole situation "as is". After reaching enough upgraded nodes, developers will make a final decision and broadcast a transaction confirming it to both networks.

## Security Considerations

If not enough nodes will upgrade to the newest version, the new rules will be rejected no matter what developers will do. Activating another hard fork without reaching enough nodes will cause another splits and make situation even worse than it currently is. The author believes that most users will download the newest version if it will be better than any of the previous ones. Even if the new rules will be rejected, having one client that can correctly handle both coins, split them if needed and mine coins under any consensus chosen by the miner should encourage enough people to upgrade and should make situation better than it currently is, if the software will be stable enough.

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).

