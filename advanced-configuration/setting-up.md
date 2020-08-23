---
description: >-
  After installation, to start sending Mailchain messages, follow the steps
  below...
---

# Advanced Set Up

## Add Account

To send and receive messages with Mailchain you will need to add an account.

Specific instructions for supported protocols can be found here:

* [Ethereum](../ethereum-instructions/setting-up.md)
* [Substrate](../substrate-instructions/setting-up.md)

```bash
mailchain account add --protocol=[PROTOCOL] --private-key=[PRIVATE-KEY-VALUE] --key-type=[KEY-TYPE]
```

* `--protocol` currently supported protocols are: `ethereum` and `substrate`.
* `--private-key`of your account to be able to sign and decrypt messages.

  `--passphrase`  can be optionally supplied in the command line or at the prompt when the application starts.

* `--key-type`  includes `secp256k1` \(default for Ethereum\), `ed25519` \(default for Substrate\), `sr25519` \(Substrate\)

{% hint style="info" %}
_Mailchain stores your private key in an encrypted format, a passphrase is required._

Enter a non-guessable passphrase, and again to confirm it. You must remember your password to decrypt the key later to send or receive messages.
{% endhint %}

{% hint style="danger" %}
You should never expose your private keys to an entity you don't trust.

Mailchain stores your private key locally, in an encrypted format. Your private keys are never sent anywhere. They are only used to decrypt messages data, and sign transactions.
{% endhint %}



