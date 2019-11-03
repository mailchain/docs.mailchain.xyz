---
title: Add Account
weight: 6
menu: true
---

To send and receive messages with Mailchain you will need to add an account. To do this you will need your private key.

```sh
mailchain account add --protocol=ethereum --private-key=[PRIVATE-KEY-VALUE]
```

- `--protocol` is the protocol used. Currently supported [ethereum].
- `--private-key` the private key value which should be added. The public key and account will be calculated.
- `--passphrase` is can be optionally supplied in the command line or at the prompt when the application starts.

*Mailchain stores your private key in an encrypted format, a passphrase is required.* Enter a non-guessable passphrase, and again to confirm it. You must remember your password to decrypt the key later.

> **ATTENTION**: You should never expose your private keys to an entity you don't trust.
> Mailchain stores your private key locally, in an encrypted format. Your private keys are never sent anywhere. They are only used to decrypt messages data, and sign transactions.