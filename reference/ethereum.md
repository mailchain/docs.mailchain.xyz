# Ethereum

Mailchain users can send messages to any Ethereum account address. This section details how the Ethereum implementation of the [Message Flow](../concepts/overview.md) is achieved.

### Networks

Mailchain supports all the common Ethereum networks

| Network | Status |
| :--- | :--- |
| Mainnet | Full |
| Ropsten | Full |
| Goerli | Full |
| Kovan | Full |
| Rinkerby | Full |

### Public Key Finder

To send an encrypted message, a public key is required. Mailchain uses the public key associated with an account address to encrypt the data, and if specified by the envelope, the message contents. This ensures the recipient is also the owner of the private key and only they can decrypt data. The public key finder searches for transactions sent by the recipient address and extracts the public key.

{% hint style="info" %}
The public key for an account address can either be calculated from a transaction signed by that account address or supplied by that account holder. In order to calculate the public key, the recipient address needs to have sent at least one Ethereum transaction.
{% endhint %}

### Sender

Ethereum transactions are used to [send](../concepts/send.md) a message.

#### Envelope

Transactions contain a `data` field that stores the [envelope](programmable-envelopes.md). Bytes can be stored in the `data` field and must be hexadecimal encoded, prefixed with `0x` as per the Ethereum specification.  Data stored in a transaction must follow the Mailchain [standard encoding format](../concepts/send.md#send-transaction):`[protocol-prefix]+[mailchain-prefix]+[envelope]`. 

| Field | Example | Notes |
| :--- | :--- | :--- |
| protocol-prefix | `0x` | Required Ethereum transaction data prefix |
| mailchain-identifier | `6d61696c636861696e` | "mailchain" encoded as hexadecimal |
| envelope | `010a82012ee10c59024c836d7ca12470b5ac74673002127ddedadbc6fc4375a8c086b650060ede199f603a158bc7884a903eadf97a2dd0fbe69ac81c216830f94e56b847d924b51a7d8227c80714219e6821a51bc7cba922f291a47bdffe29e7c3f67ad908ff377bfcc0b603007ead4bfd87ff0acc272528ca03d6381e6d0e1e2c5dfd24d521` | Envelope encoded as hexadecimal |

An example of transaction data for a Mailchain message sent on Ethereum is as follows:

```text
0x6d61696c636861696e010a82012ee10c59024c836d7ca12470b5ac74673002127ddedadbc6fc4375a8c086b650060ede199f603a158bc7884a903eadf97a2dd0fbe69ac81c216830f94e56b847d924b51a7d8227c80714219e6821a51bc7cba922f291a47bdffe29e7c3f67ad908ff377bfcc0b603007ead4bfd87ff0acc272528ca03d6381e6d0e1e2c5dfd24d521
```

The same transaction and data can be viewed on [here](https://etherscan.io/tx/0x2bf261a81e624d649450a3851df2d0639a8b98ed3bce39da14e8f318adf3edb9) on Etherscan.

####  Transaction Fields

To send a message these Ethereum transaction fields must be specified.

| Field | Type | Example | Notes |  |
| :--- | :--- | :--- | :--- | :--- |
| `nonce` | [unit64](https://golang.org/pkg/builtin/#uint64) | 8 | Sequential number that represents the number of transactions the sender account has made on the network. _Added by the client, based on last nonce._ |  |
| `gasprice` | [unit64](https://golang.org/pkg/builtin/#uint64) | 0**.**00000002 | Execution fee for sending the message. _Added by the client, based on network gas price._ |  |
| `startgas` | [\*big.Int](https://golang.org/pkg/math/big/#Int) | 30,660 | Maximum gas used for sending the transaction. Mailchain messages uses  ~30,000 GAS approx 1.5x the cost of a basic transaction. _Added by the client, based on required gas._ |  |
| `to` | [\[\]byte](https://golang.org/pkg/builtin/#byte) | `0x92d8f10248c6a3953cc3692a894655ad05d61efb` | Address of the recipient. _Added by the client, based on recipient address in message._ |  |
| `value` | [\*big.Int](https://golang.org/pkg/math/big/#Int) | `0` | Set to send zero value transactions by default |  |
| `data` | [\[\]byte](https://golang.org/pkg/builtin/#byte) | `0x6d61696c636861696e....` | Envelope data |  |

Once the transaction fields have been populated, it must be signed using the sender private key. The signed transaction bytes can then be transmitted to the ethereum network over JSON-RPC using the [eth\_sendrawtransaction](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_sendrawtransaction) method.

### Receiver

To [read](../concepts/read.md) Mailchain messages for a specific address, transactions sent to that address need to be identified. Ethereum does not natively support an address index or similar functionality that identifies all transactions sent to or from a specific address. Third parties have API's that provide this functionality, including [Etherscan.io](https://etherscan.io/).

