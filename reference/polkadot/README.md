# Substrate \(Polkadot\)

Mailchain users can send messages to any Substrate account address. This section details how the Substrate implementation of the [Message Flow](../../concepts/overview.md) is achieved.

### Networks

Mailchain plans to support substrate networks that have the Contract Substrate Runtime Module Library  enabled \([srml\_contracts](https://substrate.dev/rustdocs/v1.0/srml_contract/struct.Module.html#method.call)\).

### Public Key Finder

To send an encrypted message, a public key is required. Mailchain uses the public key associated with an address to encrypt the data, and if specified by the envelope, the message contents. This ensures the recipient is also the owner of the private key and only they can decrypt data. The public key finder decodes a recipient address from base58 and extracting the public key \(dropping the first byte and last two bytes before prepending '0x'\).

#### Example

| Field | Example |
| :--- | :--- |
| Address \(base58 encoded\) | `5EU2BwdEH8rojoKuJ16p3t1Gs8uUUp6SoaomKud2FmXBvdbp` |
| Decoded Address \(from Base58\) | `2a6a40d2c0edf1dfa67a639599dd3de2f49eb55fcd73991ba33a67debfb04b5846459b` |
| Extracting Public Key | ~~\[2a\]~~6a40d2c0edf1dfa67a639599dd3de2f49eb55fcd73991ba33a67debfb04b5846~~\[459b\]~~ |
| Public Key | `0x6a40d2c0edf1dfa67a639599dd3de2f49eb55fcd73991ba33a67debfb04b5846` |

{% hint style="info" %}
The public key for an account address can either be calculated from an address or supplied by that account holder.

Using the same private key to generate addresses on different networks produces the same public key, but a different public address.
{% endhint %}

### Sender

Mailchain uses the functionality provided by the Contract module \([srml\_contracts](https://substrate.dev/rustdocs/v2.0.0-rc5/pallet_contracts/struct.Module.html#method.call)\) \`call\` function which is similar to a standard Substrate transaction \(signed extrinsic\) with the addition of a data field \([Vec](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html)&lt;[u8](https://doc.rust-lang.org/nightly/std/primitive.u8.html)&gt;\). A substrate parachain \(or parathread\) with the Contract module enabled permits [sending](../../concepts/send.md) transactions with an envelope containing a message.

#### Envelope

Contract transactions \(signed calls\) contain a `data` field that stores the [envelope](../programmable-envelopes.md). Bytes can be stored in the `data` field and must be hexadecimal encoded, prefixed with `0x`. Data stored in a transaction must follow the Mailchain [standard encoding format](../../concepts/send.md#send-transaction):`[protocol-prefix]+[mailchain-prefix]+[envelope]`. 

~~~~

| Field | Example | Notes |
| :--- | :--- | :--- |
| protocol-prefix | 0x | Required Contract SRML `call` function data prefix |
| mailchain-identifier | `6d61696c636861696e` | "mailchain" encoded as hexadecimal |
| envelope | `010a82012ee10c59024c836d7ca12470b5ac74673002127ddedadbc6fc4375a8c086b650060ede199f603a158bc7884a903eadf97a2dd0fbe69ac81c216830f94e56b847d924b51a7d8227c80714219e6821a51bc7cba922f291a47bdffe29e7c3f67ad908ff377bfcc0b603007ead4bfd87ff0acc272528ca03d6381e6d0e1e2c5dfd24d521` | Envelope encoded as hexadecimal |

TODO

An example of transaction data for a Mailchain message sent on Edgeware is as follows:

```
?????
```

The same transaction and data can be viewed on **here** on Subscan.

/TODO

####  Transaction/ Extrinsic Fields

To send a message the following transaction fields must be specified.

| Field | Type | Example | Notes |
| :--- | :--- | :--- | :--- |
| origin | [AccountId](https://substrate.dev/rustdocs/v1.0/srml_system/trait.Trait.html#associatedtype.AccountId) |  | TODO |
| dest | [AccountId](https://substrate.dev/rustdocs/v1.0/srml_system/trait.Trait.html#associatedtype.AccountId) |  | TODO |
| value | [BalanceOf](https://substrate.dev/rustdocs/v1.0/srml_contract/type.BalanceOf.html) |  | TODO |
| gas\_limit | [Gas](https://substrate.dev/rustdocs/v1.0/srml_contract/trait.Trait.html#associatedtype.Gas) |  | TODO |
| data | [Vec](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html)&lt;[u8](https://doc.rust-lang.org/nightly/std/primitive.u8.html)&gt; |  | TODO |

Once the fields have been populated, the extrinsic must be signed using the sender private key. The signed extrinsic bytes can then be transmitted to the substrate network over JSON-RPC using the Contract module `call` function.

### Receiver

To [read](../../concepts/read.md) Mailchain messages for a specific address, Contract calls sent to that address need to be identified.

Substrate does not natively support an address index or similar functionality that identifies all transactions sent to or from a specific address. Third parties provide some of this information through a web interface \(including Subscan.io\) but as of August 2020, no APIs consistently provide a transaction index for received transactions and their data fields.

**Transaction Indexer**

Mailchain provides a simple transaction indexer which listens for transactions and filters mailchain messages for the recipient. Further details and instructions for running it can be found here: [Substrate Transaction Indexer](substrate-transaction-indexer.md).





