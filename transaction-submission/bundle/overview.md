# Overview

### Introduction

In blockchain, a Bundle refers to a group of multiple transactions packaged into an indivisible unit to ensure they are executed on-chain in a specific, predefined order. Bundles possess the following characteristics:

* Atomicity: All transactions within a Bundle are executed as an "all-or-nothing" operation. If a single transaction fails, the entire Bundle is reverted, eliminating intermediary risks such as "buying halfway" or being unable to sell.
* Strict Execution Order: The sender of the Bundle can precisely define the sequence in which the transactions are executed.
* Privacy and Attack Resistance: Bundles typically bypass the Public Mempool and are sent directly to Builders or Validators, preventing exposure to malicious MEV (Maximal Extractable Value) attacks.



### Use Cases

**Copy Trading**

In copy trading scenarios, the primary concern for followers is high entry costs caused by transaction delays. A Bundle can package the "Smart Money" original transaction and the follower's trade together. This ensures the follower's transaction immediately follows the target—executing within the same block and at the closest possible position—minimizing price slippage.

**Sniping**

At the moment a new token pool is activated, sniping transactions often face high buy-in costs due to slow on-chain inclusion. Furthermore, extreme price volatility during a launch makes these trades prime targets for malicious MEV bots. By submitting a sniping trade via a Bundle immediately after the liquidity injection transaction, users can ensure same-block execution while defending against potential MEV attacks.

**Backrunning**

In backrunning scenarios, Searchers bundle a target transaction with an arbitrage transaction in a specific order. This ensures the backrun trade is locked into the very next position after the target transaction, without fear of competitors "cutting in line." Additionally, leveraging atomicity, the Bundle only executes if both transactions are profitable within that block. If market fluctuations erase the profit margin, the Bundle fails, preventing any loss of principal.

**Approve + SWAP**

Bundles significantly enhance the Swap experience. Typically, users must execute an "Approve" transaction before they can perform a "Swap." By encapsulating these two independent transactions into a single Bundle, users only need to provide a signature once, and both steps are completed within the same block. Since the transactions do not pass through the public Mempool, malicious actors cannot predict or exploit your authorization status.
