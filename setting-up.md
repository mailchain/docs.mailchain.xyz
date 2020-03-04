---
description: >-
  After installation, to start sending Mailchain messages, follow the steps
  below...
---

# Setting Up

## Add Account

To send and receive messages with Mailchain you will need to add an account. To do this you will need a private key for an Ethereum account.

```bash
mailchain account add --protocol=ethereum --private-key=[PRIVATE-KEY-VALUE] --key-type=[KEY-TYPE]
```

* `--protocol` is the protocol which the key is added to. Currently supported `[ethereum]`.
* `--private-key` the private key value which should be added. The public key and account will be calculated.
* `--passphrase` is can be optionally supplied in the command line or at the prompt when the application starts.
* `--key-type`  includes `secp256k1` \(default for Ethereum\), `ed25519` \(default for Polkadot\), `sr25519` \(Polkadot\)

{% hint style="info" %}
_Mailchain stores your private key in an encrypted format, a passphrase is required._

Enter a non-guessable passphrase, and again to confirm it. You must remember your password to decrypt the key later to send or receive messages.
{% endhint %}

{% hint style="danger" %}
You should never expose your private keys to an entity you don't trust.

Mailchain stores your private key locally, in an encrypted format. Your private keys are never sent anywhere. They are only used to decrypt messages data, and sign transactions.
{% endhint %}

## Serve

After you have added the account, you are ready to start the application and serve the api.

To start the application, run:

```bash
mailchain serve
```

_When prompted enter the same passphrase as when you added the account._

You are now ready to start sending and receiving mails. Navigate to [https://inbox.mailchain.xyz](https://inbox.mailchain.xyz) to see your mailbox.

The Mailchain web interface has all the functionality needed to send and receive messages. It's easy and fun to use. For more information on switching between Mainnet and testnets, see [Mailchain Web Interface](mailchain-web-inbox/mailchain-web-interface.md).

