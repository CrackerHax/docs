---
description: An overview of the network's contracts with descriptions and links
---

# Fuse chain consensus

{% hint style="info" %}
All the contracts in this section are available on our [Github](https://github.com/fuseio/fuse-network/tree/master/contracts) 
{% endhint %}

#### [Consensus - 0x3014ca10b91cb3d0ad85fef7a3cb95bcac9c0f79](https://explorer.fuse.io/address/0x3014ca10b91cb3d0ad85fef7a3cb95bcac9c0f79)

This contract is responsible for handling the network DPos consensus. The contract is storing the current validator set and choosing a new validator set at the end of each cycle. The logic for updating the validator set is to select a random snapshot from the snapshots taken during the cycle.

The snapshots taken, are of pending validators, who are those which staked more than the minimum stake needed to become a network validator. Therefore the contract is also responsible for staking, delegating and withdrawing those funds.

Stake amount for a validator is the sum of staked and delegated amount to its address.

This contract is based on `non-reporting ValidatorSet` [described in Parity Wiki](https://wiki.parity.io/Validator-Set.html#non-reporting-contract).

{% hint style="info" %}
minimum stake amount = 3,000,000 Fuse token

cycle duration blocks = 1440 \(approximately 2 hours\)

snapshots taken per cycle = 10
{% endhint %}

#### [Block Reward - 0x63D4efeD2e3dA070247bea3073BCaB896dFF6C9B](https://explorer.fuse.io/address/0x63d4efed2e3da070247bea3073bcab896dff6c9b)

This contract is responsible for generating and distributing block rewards to the network validators according to the network specs \(5% yearly inflation\).

Another role of this contract is to call the snapshot/cycle logic on the Consensus contract

This contract is based on `BlockReward` [described in Parity Wiki](https://wiki.parity.io/Block-Reward-Contract).

#### [Voting - 0x4c889f137232E827c00710752E86840805A70484](https://explorer.fuse.io/address/0x4c889f137232E827c00710752E86840805A70484)

This contract is responsible for opening new ballots and voting to accept/reject them. Ballots are basically offers to change other network contracts implementation.

Only network validators can open new ballots, everyone can vote on them, but only validators votes count when the ballot is closed.

Ballots are opened/closed on cycle end.

{% hint style="info" %}
max number of open ballots = 100

max number of open ballots per validator = 100 / number of validators

minimum ballot duration \(cycles\) = 2

maximum ballot duration \(cycles\) = 14
{% endhint %}

#### [Proxy Storage](https://explorer.fuse.io/address/0x23D8634ED1B2662dC96FcE6208fde93258731333)

This contract is responsible for holding network contracts implementation addresses and upgrading them if necessary \(via voting\).

