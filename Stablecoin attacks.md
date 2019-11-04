
Cryptocurrencies are still in their infancy and are still very volatile. Stablecoins, price-stable cryptocurrencies, have thus attracted a lot of attention. They are, however, not without attack vectors.

 ## **Speculative attack**
A speculative attack is a sudden and massive selling of a currency (in our case, cryptocurrency) in a short space of time. Such an attack was launched against Tether (USDT) stablecoin [1]. The attack took 3 hours from start to finish and was launched to profit from Tether breaking its peg from the U.S Dollar.
The attack started around Sunday, October 14, 2018, 10 p.m. PST (UTC-7:00) and finished around Monday, October 15, 2018, 1 a.m. PST (UTC-7:00) and took about 100 minutes to drive the tether price to the bottom at $0.925284. Then, about 65 minutes later, the price went back to $0.973513 and started to stabilize. Even though it does not let us determine the profitability of the attack, the whole crypto market went up 10 percent, adding $20 billion in value, while at the same time, tether dropped by about 7 percent, removing only about $210 million in value

In the Tether attack, it seems that the attacker(s) :
1) first built up a big position in tether (either short or non-short position) and a big position in bitcoin or other crypto assets; 
2) then executed a massive and sudden selling of tether, which drove the tether price down to the bottom and caused the bitcoin price to go up by about 10 percent; 
3) finally sold the big bitcoin position to generate profit; and 
4) possibly bought back tether at a lower price to reduce the loss from dumping tether.

**Known Project Attack**: Tether

## **Oracle Attacks**
Oracles are a way to bring off-chain data on-chain, or bringing external data that exists from outside the cryptocurrency realm, into the cryptocurrency realm. The oracle attack is also a form of speculative attack. For a stablecoin to work, it needs to peg to, say the Dollar rate, however, that blockchain has to get that Dollar price from *somewhere*.
The oracle attack is focused on attacking the oracle in order for it to feed false/incorrect information in order to profit from the false information being executed [2]. This is dependent on knowing or determining *when* and *where* the Oracle<>Blockchain data exchange happens.

Example:
In the case of Stablecoins, one could take a short position on a stablecoin that is actually trading at $1, and feed false/incorrect price to the Oracle and thus trick the stablecoin smart contract into thinking that it is trading at $1.10, the protocol will automatically mint more tokens and the attacker profits.

**Known Project Attacks**: N/A

A solution to this potential attack is the use of *decentralized Oracles*, where nodes or token must reach consensus about certain events. However, they too are not without attack vectors, although these attack vectors are a bit harder to pull off.

## **P+Epsilon Attack**
This attack is defined thus: “a simple Schelling game where users vote on whether or not some particular fact is true (1) or false (0); say in our example that it’s actually false. Each user can either vote 1 or 0. If a user votes the same as the majority, they get a reward of P; otherwise they get 0 [3]. The theory is that if everyone expects everyone else to vote truthfully, then their incentive is to also vote truthfully in order to comply with the majority, and that’s the reason why one can expect others to vote truthfully in the first place; a self-reinforcing Nash equilibrium.“
The payoff matrix would look like this:


 |                | You vote 0    | You vote 1
 |----------------| ------------- | ------------- |
 | Others vote 0  |     P         |         0     |
 |                |               |               |
 | Others vote 1  |       0       |         P     |
 |                |               |               |





The P+Epsilon attack would be in this manner:
“Suppose that an attacker credibly commits (eg. via an Ethereum contract, by simply putting one’s reputation at stake, or by leveraging the reputation of a trusted escrow provider) to pay out X to voters who voted 1 after the game is over, where X = P + ε if the majority votes 0, and X = 0 if the majority votes 1. Now, the payoff matrix looks like this:”



 |                | You vote 0    | You vote 1
 |----------------| ------------- | ------------- |
 | Others vote 0  |     P         |       P + ε   |
 |                |               |               |
 | Others vote 1  |       0       |         P     |
 |                |               |               |


This incentivises anyone to vote 1 no matter what the majority votes for. Given that the ShellingPoint will be 1, majority will also vote for 1, meaning the attacker won’t have to pay anything and thus launch an attack at zero cost to the attacker. 

**Known Project Attacks**: 
*Kleros. Here is a contract that implements a p + epsilon attack against the Kleros court [4]
* SchellingCoin


**References**

[1] Op Ed: Anatomy of the Tether Attack: Are Stablecoins Vulnerable?[Online]. Available: https://bitcoinmagazine.com/articles/op-ed-anatomy-tether-attack-are-stablecoins-vulnerable/, Date accessed: 2019-02-12

[2] On Oracles and Schelling Points[Online]. Available: https://medium.com/witnet/on-oracles-and-schelling-points-2a1807c29b73, Date accessed: 2019-02-12

[3] The P + epsilon Attack[Online]. Available: https://blog.ethereum.org/2015/01/28/p-epsilon-attack/, Date accessed: 2019-02-20

[4] Kleros attacks[Online]. Available: https://github.com/kleros/kleros-attacks/blob/master/contracts/p-epsilon.sol, Date accessed: 2019-02-15

