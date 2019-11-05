# Types of attacks against Proof of Stake chains
Proof of stake blockchains also have certain attack types, which are different from Proof of work attack types.
The following are essentially resource exhaustion attacks on Proof of Stake blockchains.

# Fake Stake Attacks 

Fake stakes attacks work because PoSv3 implementations do not adequately validate network data before committing precious resources (disk and RAM). The consequence is that an attacker without much stake (in some cases none at all) can cause a victim node to crash by filling up its disk or RAM with bogus data

## Vulnerability #1 - No Stake Attack
In Bitcoin (and similar PoW blockchains), block propagation is split into two chunks - the block and the header, with the later going first. Nodes only ask for Block after Header passes the PoW checks AND it is a longest (or longer) chain.
Since the coinstake transaction is present only in Block but not the Header, a node cannot validate the Header on its own. Instead, it directly stores the header to an in-memory data structure (mapBlockIndex). As a result, any network attacker, even with no stake whatsoever, can fill up a victim node’s RAM.
Exploiting either of this vulnerability can be carried out without having any stake in the affected cryptocurrency at all. This attack only works against PoSv3 codebases.

**Known Project Attack**: Qtum, Particl, Navcoin, HTMLcoin, and Emercoin

## Vulnerability #2 - Spend Stake Attack
For codebases earlier than PoSv3, the following checks are made prior to storing blocks on disk:
 1) Check if the output being spent exists in the main chain
 2) Check if the PoS kernel hash meets the difficulty target
 
The first check ensures that the coin exists, but *not* that it is unspent, so this can be bypassed by using an output that is seen by the node but is already spent.

**Known Project Attack**: PIVX, PotCoin, Diamond, Blackcoin, Peercoin

## Vulnerability #3 - Stake Amplification Attack
The second check can be bypassed due to inadequate validation which could allow an attacker to amplifiy their apparent stake by creating many self-spends of the same quality coins.
For example, even with 0.01% stake in the system, the attacker only needs 5000 transactions to mine blocks with 50% apparent stake power. After the attacker has collected a large amount of apparent stake, he then proceeds to mine PoS blocks at a past time using the freshly collected apparent stake outputs. Finally, the attacker fills the disk of the victim peer with the invalid blocks.
 An attacker could buy some coins from an exchange, amplify the stake through self-spends as we described, and then sell those coins back to the exchange, performing the attack at any later date. The only cost incurred to the attacker would be the transaction fees.

**Known Project Attack**: PIVX, PotCoin, Diamond, Blackcoin, Peercoin

# Long range attacks 
A Long Range attack is a scenario where an adversary creates a branch on the blockchain starting from the Genesis block and overtakes the main chain, thus rewriting history.

The root cause of these long range or history revision attacks is due to:

**Weak Subjectivity** - this relates to new nodes and offline nodes that come online after a significant amount of time. These nodes would not be able to immediately distinguish which of the branches it received is the main chain. With Proof of Work, it's easy to determine the main chain as it is the one with the most proof of work, whereas in Proof of Steak, since there is no 'work' done, it's easier for such nodes to be deceived, atleast for a time. The longest chain rule does not work in Proof of Stake blockchains.

<insert image>

**Costless Simulation** - 
Proof of stake blockchains rely on validators and has no miners and no heavy computation, so the cost of producing up-to-date branches with the same length is so meanial that it's almost costless.

<insert image>

It is these two aspects that long range attacks exploits in Proof of Stake blockchains.
There are **four types of long range attacks**:

Simple, Posterior Corruption, Liveness Denial and Stake Bleeding.

## **Simple**
This simple long range attack is due to validator nodes not checking block timestamps.
An example of this would be, assuming the validator pool has 3 validators (A,B,C) with equal stake, if validator node A forks the blockchain from the genesis block and mints her branch. But since the details about validators and their stake is in the genesis block, validator A would not be able to produce blocks faster than the main chain. The one way to produce blocks faster than the main chain would be for validator A to forge block timestamps in that branch. In PoS implementations where nodes don't validate block timestamps, the main chain branch and validator A's forged branch would be valid and other nodes would not be able to detect the difference.

<insert image>
 
 **mitigation**
 block timestamp mitigation

## **Posterior Corruption**
In Proof of Stake blockchains, there is a concept of validator rotation which allows every validator a chance to produce blocks. In this attack example, suppose validator B has signed a few thousand blocks and decides to cash out her stake. While validator cannot ever sign new blocks, he can still resigning the few thousand blocks she already signed, in the event that she needs to sign those same blocks in a different branch.
In this scenario, validator A can coerce validator B to sign the blocks in validator A's branch; validator B has nothing to loose in this regard and, if she agrees, each time validator B is elected to produce blocks, she produces blocks in validator A's branch. This action allows validator A to have a longer branch than the main chain branch due to validator B signing her branch. This is called a Posterior Corruption attack.

<insert image>
 
 **mitigation**:
 Key-evolving cryptography and moving checkpoints.
 
 ## **Liveness Denial**
 This attack is dependant on the stake that a validator has. It happens when a validator forfeits her turn to produce blocks, however, forfeiting her chance doesn't mean another validator takes her spot, it just means for that no blocks will be produced during that validators period.

**mitigation**:
Modify the proof of stake algorithms that gradually reduces non-participating nodes' weights in the validator set if they do not participate in consensus 

# Nothing at stake
This attack relies on the assumption of "cheap" (almost nothing) mining on forks of the same PoS (Proof of Stake) chain. It's assumed that as little as 1% of network stake purchase could yeild a succesful attack, compared to 51% in Proof of Work chains.
Make sense of it in this scenario : 1 chain forks into chain A and chain B. A validator builds on both forks and from chain A, sends the fork coin to an exchange and trades it for Bitcoin, Ethereum, etc. Then the validator forsakes building on chain A (because she already got her Bitcoin,Ethereum, etc) and focuses on building on chain B. This chain B stands a greater chance of being the accepted chain and she thus profited from chain A and will at some point profit from chain B

**Known Project Attack**: N/A
