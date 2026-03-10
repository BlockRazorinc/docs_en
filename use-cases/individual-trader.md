# Individual Trader

## Introduction

{% hint style="info" %}
Individual users can use general RPC without subscribing to a plan.
{% endhint %}

For users who frequently trade on DEXs, there is a high probability that their trades will execute at the maximum slippage limit, resulting in "invisible" financial losses. Individual traders can now [add](individual-trader.md#how-to-add-rpc-to-my-wallet) the BlockRazor RPC to their wallets with a single click. From then on, all initiated swap transactions will benefit from the deep protection of the BlockRazor RPC, reducing slippage losses while offering the opportunity to receive real-time transaction rebates. Currently, BlockRazor supports RPC integration for individual traders on Ethereum and BSC.

Advanced users can choose to [add different modes of the RPC](individual-trader.md#how-to-add-custom-rpc-to-wallet) according to your needs. If you have any questions, please contact us on [Discord](https://discord.com/invite/qqJuwRb8Nh).



### How to add RPC to my Wallet

#### Metamask

1. Go to [rpc.blockrazor.io](https://rpc.blockrazor.io), click on **GET PROTECTED**

<figure><img src="../.gitbook/assets/image (49).png" alt="" width="563"><figcaption></figcaption></figure>

2. Click on **Connect Metamask**, and **comfirm** the connection in Metamask

<figure><img src="../.gitbook/assets/image (50).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (51).png" alt="" width="353"><figcaption></figcaption></figure>

3. Click on **Click to Add Default RPC**, and **approve** the addition of a new network in Metamask

<figure><img src="../.gitbook/assets/image (53).png" alt="" width="323"><figcaption></figcaption></figure>





### Other Wallets(using Coinbase as an example)

1. Click on the browser extension to invoke the Coinbase Wallet
2. Click on **Settings** - **Networks**

<figure><img src="../.gitbook/assets/image (54).png" alt="" width="369"><figcaption></figcaption></figure>

3. Click on **+** to add network.

<figure><img src="../.gitbook/assets/image (56).png" alt="" width="365"><figcaption></figcaption></figure>

4. Enter the network information of MEV Protect RPC General for Wallet User and click **Save**

<figure><img src="../.gitbook/assets/image (42).png" alt="" width="355"><figcaption></figcaption></figure>



### How to add custom RPC to wallet

#### Metamask

1. Go to [rpc.blockrazor.io](https://rpc.blockrazor.io), click on **GET PROTECTED**
2. Click on **Connect Metamask**, and **comfirm** the connection in Metamask
3. Click on **Click to Add Custom RPC**，choose [RPC mode](individual-trader.md#comparison-of-rpc)

<figure><img src="../.gitbook/assets/image (39).png" alt="" width="563"><figcaption></figcaption></figure>

4. Confirm the RPC mode, click on **Click to Add,** and approve the addition of the new network in the Metamask



#### Other Wallets(using Coinbase as an example)

1. Click on the browser extension to invoke the Coinbase Wallet
2. Click on **Settings** - **Networks**
3. Click on **+** to add network
4. Fill in the [RPC network information](individual-trader.md#network-information). If you need to choose the RPC mode, see [Comparison of RPC](individual-trader.md#comparison-of-rpc) for details.

<figure><img src="../.gitbook/assets/image (43).png" alt="" width="350"><figcaption></figcaption></figure>

5. Click on **Save** to complete the RPC addition.



### Network information

<table><thead><tr><th width="200"></th><th>Ethereum</th><th>BSC</th></tr></thead><tbody><tr><td>Network Name</td><td>Ethereum Mainnet</td><td>BNB Smart Chain Mainnet</td></tr><tr><td>RPC URL</td><td>https://eth.blockrazor.xyz</td><td>https://bsc.blockrazor.xyz</td></tr><tr><td>Chain ID</td><td>1</td><td>56</td></tr><tr><td>Currency Symbol</td><td>ETH</td><td>BNB</td></tr><tr><td>Block Explorer URL</td><td><a href="https://etherscan.io">https://etherscan.io</a></td><td><a href="https://bscscan.com">https://bscscan.com</a></td></tr></tbody></table>



### Comparison of RPC

<table><thead><tr><th width="146"></th><th>default</th><th>fullprivacy</th><th>maxbackrun</th></tr></thead><tbody><tr><td>BSC</td><td>https://bsc.blockrazor.xyz</td><td>https://bsc.blockrazor.xyz/fullprivacy</td><td>https://bsc.blockrazor.xyz/maxbackrun</td></tr><tr><td>Ethereum</td><td>https://eth.blockrazor.xyz</td><td>https://eth.blockrazor.xyz/fullprivacy</td><td>https://eth.blockrazor.xyz/maxbackrun</td></tr><tr><td>MEV Protection</td><td>Protected</td><td>Protected</td><td>Protected</td></tr><tr><td>Transaction Privacy</td><td>Minimal Disclosure</td><td>Full Privacy</td><td>Maximum Disclosure</td></tr><tr><td>Refund Probability</td><td>Moderate</td><td>No refunds</td><td>High</td></tr><tr><td>Refunds</td><td>Supported</td><td>No refunds</td><td>Supported</td></tr><tr><td>Revert Protection</td><td>Not Protected</td><td>Protected</td><td>Protected</td></tr></tbody></table>

**default**

* In default mode, transactions submitted to MEV Protect RPC General for Wallet User only disclose necessary transaction data (hash, logs & state) to Searcher to win refund opportunities while protecting transaction privacy to the greatest extent. At the same time, in order to ensure the speed of transactions being included in blocks, transactions are not under revert protection  (which is consistent with the default RPC of wallet).&#x20;

**fullprivacy**

* In fullprivacy mode, transactions submitted to MEV Protect RPC General for Wallet User will not disclose any transaction data, and Scutum will directly forward the transaction to the mainstream builders. Transactions in this mode are under revert protection. In order to ensure the speed of inclusion in blocks, it is recommended to set priority fee (Ethereum) when sending transactions.

**maxbackrun**

* In the maxbackrun mode, transactions submitted to MEV Protect RPC General for Wallet User will disclose necessary transaction data (hash, to, calldata, functionSelector, logs & state) under the premise of MEV protection to maximize the possibility of obtaining refunds. Transactions are under revert protection. In order to ensure the speed of inclusion in blocks, it is recommended to set priority fee (Ethereum) when sending transactions.



