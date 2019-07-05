# Getting Started

In this guide, we’ll walk you through how to install Mailchain onto your machine. Then we’ll setup the application to send, then receive messages.

Installing Mailchain is easy:  
  First, you install the application onto your local machine.  
  Then you’ll add a private key to send and receive messages.  
  Then, you can then navigate to the web interface [https://inbox.mailchain.xyz](https://inbox.mailchain.xyz) and start working.

We’ll walk you through this process step by step...

## Quick Install

To install Mailchain for the first time, run the following command to download and install the application on your local machine.

```bash
curl -sL https://run.mailchain.xyz/install.sh | sh
```

## Manual Install

To choose where to store the application, you can install mailchain manually.

### 1. Download the application

Download the application directly via the [Mailchain releases](https://github.com/mailchain/mailchain/releases/latest) page. We recommend you save it in your home directory: `~/.mailchain/bin`

### 2. Export the application path

Next, add mailchain to your environmental variable path with:

```bash
export PATH=$PATH:$HOME/.mailchain/bin
```

{% hint style="info" %}
Note: if you changed the location of the mailchain executable, you should update the path as appropriate:

```bash
export PATH=$PATH:$HOME/{mailchain_executable_location}
```
{% endhint %}

Verify the application is installed and running correctly with: `mailchain version`. For example:\`

```bash
$ mailchain version
Version: v0.0.11
```

Next, if the application is working as expected, you’ll want to add the path to `~/.profile`, `.zshrc`, or `~/.bash_profile`, depending on which shell you use.

To determine the shell you use, run `echo $SHELL`. For example, if using zsh, as shown below:

```bash
$ echo $SHELL
```

| Shell output | Command to export the path to the shell profile |
| :--- | :--- |
| /bin/zsh | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.zshrc` |
| /bin/bash | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.bashrc` |
| /bin/ksh | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.kshrc` |

You are now ready to [initialize](getting-started.md#initialize) the application.

## Initialize

When using Mailchain for the first time you need to initialize the application by running:

```bash
mailchain init
```

This configures Mailchain with the default settings. If you wish to view those settings you can view the `.mailchain.yaml` file in the `~/.mailchain` directory. 

You can change configuration settings to use your own [storage](advanced-configuration/advanced-storage-configuration.md) or blockchain [endpoints](advanced-configuration/advanced-ethereum-json-rpc-endpoint-configuration.md).

Running `mailchain init` again will give you the option to remove the current file and start over.

## Add Account

To send and receive messages with Mailchain you will need to add an account. To do this you will need your private key.

```bash
mailchain account add --chain=ethereum --private-key=[PRIVATE-KEY-VALUE]
```

* `--chain` is the chain which the key is added to. Currently supported `[ethereum]`.
* `--private-key` the private key value which should be added. The public key and account will be calculated.
* `--passphrase` is can be optionally supplied in the command line or at the prompt when the application starts.

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

You are now ready to start sending and receiving mails. Navigate to [https://inbox.mailchain.xyz](https://inbox.mailchain.xyz) to see your mailbox. The Mailchain web interface has all the functionality needed to send and receive messages. It's easy and fun to use.

