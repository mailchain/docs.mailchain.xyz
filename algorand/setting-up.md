# Setting Up

## Add Account

To send and receive messages with Mailchain on Algorand, you will need to add an existing account \(or create a new one and save the 25 word mnemonic phrase\).

```text
mailchain account add --protocol=algorand --network=[NETWORK] --private-key-encoding=mnemonic/algorand --private-key=[PRIVATE-MNEMONIC-STRING-VALUE] --key-type=ed25519
```

* `--network=mainnet`  or a testnet you are working on.
* `--private-key-encoding=mnemonic/algorand` is the encoding used for supplied private key
* `--private-key` is the 25 word mnemonic phrase of your account to be able to sign and decrypt messages.
* `--key-type=ed25519` \(for Algorand\).

{% hint style="info" %}
_Mailchain stores your private key/ mnemonic phrase in an encrypted format, a passphrase is required._

Enter a non-guessable passphrase, and again to confirm it. You must remember your password to decrypt the key later to send or receive messages.
{% endhint %}

{% hint style="danger" %}
You should never expose your private keys mnemonic phrase to an entity you don't trust.

Mailchain stores your private key locally, in an encrypted format. Your private keys are never sent anywhere. They are only used to decrypt messages data, and sign transactions.
{% endhint %}

## Mailchain Settings

By default, Mailchain comes preconfigured with some default values to make it easier to get started. [Algoexplorer](https://algoexplorer.io/) is configured by default to query the received messages.

To change the API lookup settings in the Mailchain Client, follow the instructions here: [Mailchain Settings: Viewing and Updating](../advanced-configuration/mailchain-settings-viewing-and-updating.md)



