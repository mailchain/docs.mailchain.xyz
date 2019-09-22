---
description: This page is currently a draft spec. Please don't use yet.
---

# Polkadot \(draft\)

Mailchain users can send messages to any Polkadot account address. This section details how the Polkadot implementation of the [Message Flow](../concepts/overview.md) is achieved.

### Networks

Mailchain plans to support the following Polkadot networks

| Network | Status |
| :--- | :--- |
| Polkadot \(Mainnet\) | Pending |
| Kusama \(Canary Network\) | Pending |
| Alexander \(Testnet\) | Pending |

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

The Mailchain Substrate Runtime Module Library \(srml-mailchain\) is similar to a standard Substrate transaction \(signed extrinsic\) with the addition of a data field \[TODO: add link to data field details and type; likely to be [Vec](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html)&lt;[u8](https://doc.rust-lang.org/nightly/std/primitive.u8.html)&gt; similar to [srml-contracts](https://substrate.dev/rustdocs/v1.0/srml_contract/struct.Module.html#method.call)\]. The srml is used to [send](../concepts/send.md) a transaction with an envelope containing a message.

#### Envelope

~~Transactions contain a `data` field that stores the~~ [~~envelope~~](programmable-envelopes.md)~~.~~

~~TODO: Bytes can be stored in the `data` field~~

~~TODO: Does this need to be encoded/ prefixed?~~

 ~~TODO: Confirm:~~Data stored in a transaction must follow the Mailchain [standard encoding format](../concepts/send.md#send-transaction):`[protocol-prefix]+[mailchain-prefix]+[envelope]`. 

~~~~

| Field | Example | Notes |
| :--- | :--- | :--- |
| protocol-prefix | 0x \[TBC\] | Required Mailchain SRML transaction data prefix |
| mailchain-identifier | `6d61696c636861696e` | "mailchain" encoded as hexadecimal |
| envelope | `?????` | Envelope encoded as hexadecimal |

TODO: An example of transaction data for a Mailchain message sent on \[INSERT TESTNET HERE\] is as follows:

```
?????
```

TODO: The same transaction and data can be viewed on ~~**here**~~ on Polkascan.

####  Transaction/ Extrinsic Fields

To send a message the following transaction fields must be specified.

| Field | Type | Example | Notes |
| :--- | :--- | :--- | :--- |
| origin | [AccountId](https://substrate.dev/rustdocs/v1.0/srml_system/trait.Trait.html#associatedtype.AccountId) |  | TODO |
| dest | [AccountId](https://substrate.dev/rustdocs/v1.0/srml_system/trait.Trait.html#associatedtype.AccountId) |  | TODO |
| value | [BalanceOf](https://substrate.dev/rustdocs/v1.0/srml_contract/type.BalanceOf.html) |  | TODO |
| gas\_limit | [Gas](https://substrate.dev/rustdocs/v1.0/srml_contract/trait.Trait.html#associatedtype.Gas) |  | TODO |
| data | [Vec](https://doc.rust-lang.org/nightly/alloc/vec/struct.Vec.html)&lt;[u8](https://doc.rust-lang.org/nightly/std/primitive.u8.html)&gt; |  | TODO |

~~Once the transaction fields have been populated, it must be signed using the sender private key. The signed transaction bytes can then be transmitted to the substrate network over JSON-RPC using the \[INSERT SRML RPC METHOD HERE~~\] ~~method.~~

### Receiver

~~To~~ [~~read~~](../concepts/read.md) ~~Mailchain messages for a specific address, transactions sent to that address need to be identified. Substrate does not natively support an address index or similar functionality that identifies all transactions sent to or from a specific address. Third parties have API's that provide this functionality, including Polkascan \[TODO: confirm polkascan api reqs\].~~

