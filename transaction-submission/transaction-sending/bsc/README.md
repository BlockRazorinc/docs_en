---
description: >-
  Introduction to BlockRazor BSC Transaction Sending Mode and API Integration
  Documentation
---

# BSC Transaction Sending

### What is Broadcast Tx

Broadcast Tx is a fast transaction sending service provided by BlockRazor to help users send transactions with lower latency. It is part of the Fast ecosystem, but unlike the standard Fast model which requires attaching a tip to the transaction, Broadcast Tx does not require users to pay extra for a tip within the transaction, making it more suitable as a low-barrier, fast sending entry point.

Currently, Broadcast Tx offers two methods: `SendTx` and `SendTxs`, which are used to send single transactions and batch transactions.

It's important to note that while Broadcast Tx belongs to the Fast ecosystem, it is not equivalent to a private transmission channel with full transaction protection capabilities. Transactions sent via Broadcast Tx still enter the public propagation path and therefore _DO NOT_ have MEV protection capabilities.

### In what scenarios should you choose Broadcast Tx

* No tips needed, lower barrier to entry\
  Unlike the standard Fast model, Broadcast Tx does not require adding tips to transactions, making it more suitable for users who want to quickly integrate but do not want to modify the transaction incentive structure.
* Suitable for scenarios where speed is a requirement but MEV protection is not currently emphasized\
  If your priority is to send transactions out as quickly as possible, rather than hiding transactions or mitigating risks like sandwiches and frontrunnings through private paths, then Broadcast Tx would be a more straightforward option.

### Benchmark

In our benchmark on transaction inclusion latency, we conducted multiple rounds of comparisons between BlockRazor and regular Nodes in four regions: Dublin, Frankfurt, Tokyo, and Virginia. The evaluation criteria consisted of two layers: first, comparing whether the transaction is included in the earlier block; second, if both transactions were included within the same block, we further compared the order of their transaction indices. The results are as follows:

<table><thead><tr><th width="187.37109375">Region</th><th width="511.00390625">BlockRazor Total Lead Rate</th></tr></thead><tbody><tr><td>Dublin</td><td><strong>88.7%</strong><br><strong>-</strong> Same block but better index: 82.9%<br>- Earlier block: 5.8%</td></tr><tr><td>Frankfurt</td><td><strong>85.4%</strong><br><strong>-</strong> Same block but better index: 81.3%<br>- Earlier block: 4.2%</td></tr><tr><td>Tokyo</td><td><strong>85.1%</strong><br><strong>-</strong> Same block but better index: 78.7%<br>- Earlier block: 6.4%</td></tr><tr><td>Virginia</td><td><strong>97.9%</strong><br><strong>-</strong> Same block but better index: 95.7%<br>- Earlier block: 2.1%</td></tr></tbody></table>

In terms of percentage results, BlockRazor maintained a higher overall lead across all regions. In the Dublin region, BlockRazor led by 88.7%, in Frankfurt by 85.4%, in Tokyo by 85.1%, and in Virginia by a remarkable 97.9%.

Looking further at the leading mechanism, BlockRazor's advantages are mainly reflected in two aspects: First, in most leading rounds, even when entering the same block as a regular Node, BlockRazor still obtains a higher transaction index; second, in some rounds, BlockRazor can even directly complete transaction inclusion one block ahead. This indicates that BlockRazor not only has a greater chance of entering earlier block windows, but also has a better chance of achieving a superior ranking position in the competition for the same block, thus forming a stable submission advantage.
