# Start for free

{% hint style="info" %}
BlockRazor offers new registered users multi-mode transaction sending services on Solana, BSC, Etherem, Base, including RPC, Fast, Bundle, and Block Builder modes for free.
{% endhint %}

### RPC

<table><thead><tr><th width="125.16015625">Chain</th><th>Methods</th><th>Limit</th></tr></thead><tbody><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/rpc/bsc/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li><li><a href="../transaction-submission/rpc/bsc/eth_sendmevbundle/"><code>eth_sendMevBundle</code></a></li><li>Other JSON RPC methods</li></ul></td><td>-</td></tr><tr><td>Ethereum</td><td><ul><li><a href="../transaction-submission/rpc/ethereum/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li><li><a href="../transaction-submission/rpc/ethereum/eth_sendbundle.md"><code>eth_sendBundle</code></a></li><li>Other JSON RPC methods</li></ul></td><td>-</td></tr><tr><td>Base</td><td><ul><li><a href="../transaction-submission/rpc/base/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li></ul></td><td>1 Tx / 5s</td></tr></tbody></table>

### Block Builder

<table><thead><tr><th width="125.484375">Chain</th><th width="288.10546875">Methods</th><th>Limit</th></tr></thead><tbody><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/block-builder/send-bundle.md">eth_sendBundle</a></li><li><a href="../transaction-submission/block-builder/send-privatetransaction.md">eth_sendPrivateTransaction</a></li></ul></td><td>-</td></tr></tbody></table>

### Fast

<table><thead><tr><th width="113.1328125">Chain</th><th>Methods</th><th>Limit</th></tr></thead><tbody><tr><td>Solana</td><td><ul><li><a href="../transaction-submission/fast/solana/send-transaction/"><code>Send Transaction</code></a> </li><li><a href="../transaction-submission/fast/solana/send-bundle/"><code>Send Bundle</code></a></li><li><a href="../transaction-submission/fast/solana/send-batch/"><code>Send Batch</code></a></li></ul></td><td>-</td></tr><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/fast/bsc/broadcast-tx.md"><code>Broadcast Tx</code></a></li></ul></td><td><ul><li>TPS：10 Txs / 5s</li><li>Daily Tx Limit：10</li></ul></td></tr><tr><td>Base</td><td><ul><li><a href="../transaction-submission/fast/base/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li></ul></td><td>Default to 10 TPS</td></tr></tbody></table>
