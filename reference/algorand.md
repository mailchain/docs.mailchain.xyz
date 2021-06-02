# Algorand

Mailchain users can send messages to any Algorand account address. This section details how the Algorand implementation of the [Message Flow](../concepts/overview.md) is achieved.

### Networks

Mailchain supports all the public Algorand networks

| Network | Status |
| :--- | :--- |
| Mainnet | Full |
| BetaNet | Full |
| TestNet | Full |

### Public Key Finder

To send an encrypted message, a public key is required. Mailchain uses the public key associated with an account address to encrypt message data, and if specified by the envelope, the message contents too. This ensures the recipient is also the owner of the private key and only they can decrypt data. The public key finder returns the public key for a recipient public address.

{% hint style="info" %}
The public key for an account address can be calculated from the public address by converting it from its Base32 encoded representation to Base58 and removing the 4-byte checksum.
{% endhint %}

### Sender

Algorand transactions are used to [send](../concepts/send.md) a message.

#### Envelope

Transactions contain a `note` field that stores the [envelope](programmable-envelopes.md). Bytes can be stored in the `note` field and can be any data up to 1000 bytes. Data stored in a transaction must follow the Mailchain [standard encoding format](../concepts/send.md#send-transaction):`[protocol-prefix]+[mailchain-prefix]+[envelope]`. This data will be encoded to Base64 when transmitted.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">protocol-prefix</td>
      <td style="text-align:left">None</td>
      <td style="text-align:left">
        <p>Transaction data prefix is not required for Algorand.</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mailchain-identifier</td>
      <td style="text-align:left"><code>bWFpbGNoYWlu</code>
      </td>
      <td style="text-align:left">&quot;mailchain&quot; encoded as base64</td>
    </tr>
    <tr>
      <td style="text-align:left">envelope</td>
      <td style="text-align:left"><code>AQpuKuI/nZUw6qvRDt+/aAUOqu7J72/CZMc+kPsbVrCTq1MB9JwTVJadZJLB4h07XEon6Yf9ubvaxTTHAltoFjyWipQzyuxFfP1I8Y5OZE4dUFsEheF2jN8DUfKwpQKEKILoySTH6a4VhWwq8R1T3/0SBiIEsORJjw</code>
      </td>
      <td style="text-align:left">Envelope encoded as hexadecimal</td>
    </tr>
  </tbody>
</table>

An example of a transaction `note` field for a Mailchain message sent on Algorand is as follows:

```text
bWFpbGNoYWluAQpuKuI/nZUw6qvRDt+/aAUOqu7J72/CZMc+kPsbVrCTq1MB9JwTVJadZJLB4h07XEon6Yf9ubvaxTTHAltoFjyWipQzyuxFfP1I8Y5OZE4dUFsEheF2jN8DUfKwpQKEKILoySTH6a4VhWwq8R1T3/0SBiIEsORJjw==
```

The same transaction and data can be viewed [here](https://testnet.algoexplorer.io/tx/YA6BWUPKZGT237Y7MTDJHEKOZKRAQPTF7YY2EENBQGQWU7TWJFVA) on [Algoexplorer](https://algoexplorer.io/).

####  Transaction Fields

To send a message the following Algorand transaction fields must be specified.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Codec</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Notes</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Fee</td>
      <td style="text-align:left"><code>fee</code>
      </td>
      <td style="text-align:left"><a href="https://golang.org/pkg/builtin/#uint64">uint64</a>
      </td>
      <td style="text-align:left">1000</td>
      <td style="text-align:left">Paid by the sender to the FeeSink to prevent denial-of-service. The minimum
        fee on Algorand is currently 1000 microAlgos.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">FirstValid</td>
      <td style="text-align:left"><code>fv</code>
      </td>
      <td style="text-align:left"><a href="https://golang.org/pkg/builtin/#uint64">uint64</a>
      </td>
      <td style="text-align:left">6000000</td>
      <td style="text-align:left">The first round for when the transaction is valid. If the transaction
        is sent prior to this round it will be rejected by the network.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">LastValid</td>
      <td style="text-align:left"><code>lv</code>
      </td>
      <td style="text-align:left"><a href="https://golang.org/pkg/builtin/#uint64">uint64</a>
      </td>
      <td style="text-align:left">6001000</td>
      <td style="text-align:left">The ending round for which the transaction is valid. After this round,
        the transaction will be rejected by the network.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">GenesisHash</td>
      <td style="text-align:left"><code>gh</code>
      </td>
      <td style="text-align:left">[32]byte</td>
      <td style="text-align:left">&quot;mainnet-v1.0&quot;</td>
      <td style="text-align:left">The hash of the genesis block for the network for which the transaction
        is valid. See Algorand developer documentation for details of the genesis
        hash for MainNet, TestNet, and BetaNet.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Sender</td>
      <td style="text-align:left"><code>snd</code>
      </td>
      <td style="text-align:left">
        <p>Address</p>
        <p>(string)</p>
      </td>
      <td style="text-align:left"><code>G2GTKMEEEEZH5TFUDYZMWWGXZLO3Z7765CR52ZXBBNCCMNPDYM3ZII7CSI</code>
      </td>
      <td style="text-align:left">
        <p>The address of the account that sends the messages and pays the fee.</p>
        <p><em>Added by the client, based on sender address in message.</em>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Receiver</td>
      <td style="text-align:left"><code>rcv</code>
      </td>
      <td style="text-align:left">
        <p>Address</p>
        <p>(string)</p>
      </td>
      <td style="text-align:left"><code>UWH6MCLMZSD2UYWTJVKFKX6JMTX2TGXAOYPUBNHFFQFBBVJULXJXZJNPBU</code>
      </td>
      <td style="text-align:left">
        <p>The address of the account that receives the message.</p>
        <p><em>Added by the client, based on recipient address in message.</em>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">TxType</td>
      <td style="text-align:left"><code>type</code>
      </td>
      <td style="text-align:left"><a href="https://golang.org/pkg/builtin/#string">string</a>
      </td>
      <td style="text-align:left">&quot;pay&quot;</td>
      <td style="text-align:left">Specifies the type of Algorand transaction. <em>Mailchain uses a zero-value payment transaction by default.</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Note</td>
      <td style="text-align:left"><code>note</code>
      </td>
      <td style="text-align:left">[]byte</td>
      <td style="text-align:left"><code>bWFpbGNoYWluAQpuKuI/nZUw6qvRDt+/aAUOqu7J72/CZMc+kPsbVrCTq1MB9JwTVJadZJLB4h07XEon6Yf9ubvaxTTHAltoFjyWipQzyuxFfP1I8Y5OZE4dUFsEheF2jN8DUfKwpQKEKILoySTH6a4VhWwq8R1T3/0SBiIEsORJjw==</code>
      </td>
      <td style="text-align:left">Envelope data</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Amount</td>
      <td style="text-align:left"><code>amt</code>
      </td>
      <td style="text-align:left"><a href="https://golang.org/pkg/builtin/#uint64">uint64</a>
      </td>
      <td style="text-align:left"><code>0</code>
      </td>
      <td style="text-align:left">
        <p>The total amount to be sent in microAlgos.</p>
        <p><em>Mailchain sets this to <code>0</code> (zero).</em>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

Once the transaction fields have been populated, it must be signed using the sender private key. The signed transaction bytes can then be transmitted to the Algorand network via the Algorand network API endpoint using the `POST` [/v2/transactions](https://developer.algorand.org/docs/reference/rest-apis/algod/v2/#post-v2transactions) method.

### Receiver

To [read](../concepts/read.md) Mailchain messages for a specific address, transactions sent to that address need to be identified. The Algorand indexer natively supports an address index to identify all transactions sent to a specific address.

