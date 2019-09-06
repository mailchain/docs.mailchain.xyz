# Send

Messages are sent by creating a transaction with the data field containing an encoded [envelope](../reference/programmable-envelopes.md). Each blockchain protocol may have differences in the way data and transactions are handled. Mailchain uses a standard format plus any protocol specifics.‌

### Compose Message

In the [web interface](../mailchain-web-inbox/mailchain-web-interface.md), a user composes a message which is sent to the Mailchain client via an API, messages can also be sent programmatically via the API. The following fields are available to compose a message:

**Fields**

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| To | Encoded Address | Recipient public address | `0xd5ab4ce3605cd590db609b6b5c8901fdb2ef7fe6` |
| From | Encoded Address | Sender public address | `0x92d8f10248c6a3953cc3692a894655ad05d61efb` |
| Reply-To | Encoded Address _\(Optional\)_ | Public address responses should be sent to \[optional\] | `0x92d8f10248c6a3953cc3692a894655ad05d61efb` |
| Subject | String | Message subject | ​Hello world |
| Body | String | Message body | ​This is my first Mailchain message |
| Public Key | Encoded Public Key | The recipient public key | `0x69d908510e355beb1d5bf2df8129e5b6401e1969891e8016a0b2300739bbb00687055e5924a2fd8dd35f069dc14d8147aa11c1f7e2f271573487e1beeb2be9d0` |

{% hint style="info" %}
To determine the recipient public key, an existing transaction needs to have been sent on the blockchain by that Ethereum account. For example, to determine Bob’s public key, Bob needs to have sent a transaction.‌
{% endhint %}

### Message Preparation

Before sending the message it needs to be prepared. The Mailchain client handles this by [building fields](send.md#add-fields), [generating a contents hash](send.md#generate-contents-hash), and [encrypting the contents](send.md#encrypt-contents).

#### Message Fields

The client adds the following fields to each message:

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| Date | [RFC1123](https://tools.ietf.org/html/rfc1123) date format | Date and time of message  | `2019-04-12T18:21:00+01:00` |
| Message-ID | String | A unique message id composed of 64 chars \(32 bytes\) + `@mailchain` | `40fb138807253554afc5161740ca3dade11db7e74e799c9f6091b904277cb9b839393802dc38b8a815615543@mailchain` |
| Content-Type | String [RFC6532](https://tools.ietf.org/html/rfc6532) content type | Describe the contents of the message | `text/plain; charset="UTF8"` |
| Content-Transfer-Encoding | String | The message body is encoded according to this field | `quoted-printable` |

#### ‌Contents Hash Generation

The [contents hash](../reference/programmable-envelopes.md#contentshash) is used to verify the message has not changed since being sent. To generate the hash, the message is encoded using the specified method in the `Content-Type` and `Content-Type-Encoding` fields into a bytes representation. The bytes representation is then passed to the hash function.

{% hint style="info" %}
Contents hash provides cryptographic proof to check the message has not changed from when it was initially included in a transaction. The default hash function is`SHA3-256.`
{% endhint %}

#### Content Encryption

The message is encrypted using the recipient public key, the default encryption method is `AES-256-CBC`. The encrypted message can only be decrypted by the owner of the private key that corresponds to the public key.

An [integrity hash](../reference/programmable-envelopes.md#integrityhash) is created from the encrypted message, providing a basic integrity protection layer prior to message decryption.

{% hint style="info" %}
Integrity hash is intended to ensure the message has not been tampered with before attempting to decrypt the message. No cryptographic proof is required for this hash, the default method is`murmur3.`
{% endhint %}

### Message Transmission

To complete sending the message to a recipient, the client will [store the message](send.md#store-message), [create an envelope](send.md#create-envelope), and [send a transaction](send.md#send-transaction).

#### Store Message

A consistent characteristic of blockchain protocols is that storing bytes has a cost. Mailchain messages are stored 'off-chain' to minimise the costs of storing messages 'on-chain'. The [Mailchain specification](https://github.com/mailchain/mailchain-specification/blob/master/mailchain_specification.md#message-storage) details the requirements for a message store.

#### Create Envelope

[Programmable envelopes](../reference/programmable-envelopes.md) provide a specific wrapper around each message. Envelopes differ in functionality to support different message use cases. Envelopes are marshalled into bytes and can be encoded per the blockchain protocol encoding requirements. 

#### Send Transaction

To transmit the message to the recipient, a transaction is sent from the message sender to the message recipient. These transactions are similar to standard transactions with the exception that the `data` or equivalent type of field is used. The information included in this data field includes: a protocol prefix followed by the mailchain prefix, and then the envelope represented as bytes.

The following fields are then encoded to build the transaction data:

| Field | Description | Example |
| :--- | :--- | :--- |
| protocol-prefix | _Optional and varies per protocol_ | `0x` for Ethereum |
| mailchain-identifier | "mailchain" encoded | `6d61696c636861696e` hex encoded |
| envelope | Bytes of envelope |  |

The data is combined as `[protocol-prefix]+[mailchain-prefix]+[envelope]`

To send the transaction, the remaining transaction fields need to be supplied, before it is signed and transmitted as per the protocol requirements.[  
](https://app.gitbook.com/@mailchain/s/mailchain/~/drafts/-LmkujL2pCds-laZEl8b/primary/reference/ethereum)

