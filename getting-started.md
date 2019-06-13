# Getting Started

In this guide, we’ll walk you through how to install Mailchain onto your machine. Then we’ll setup the application to send, then receive messages.

Installing Mailchain is easy. First, you first install the application onto your local machine. Using this application, you’ll can then navigate to the web interface [https://mailchain.xyz/inbox](https://mailchain.xyz/inbox). Finally, you’ll add a private key to send and receive messages.

We’ll walk you through this process step by step.

## Install

If this is your first time running Mailchain, you’ll need to download the application onto your local machine. You’ll use this application to interact with the blockchain to send and receive messages.

Installing Mailchain is fast and easy.

To install the application, run:

```bash
curl -sL https://run.mailchain.xyz/install.sh | sh
```

Alternatively, you can download the application directly via the [Mailchain releases](https://github.com/mailchain/mailchain/releases/latest) page.

Next, add mailchain to your path with:

```bash
export PATH=$PATH:$HOME/.mailchain/bin
```

Verify the application is installed and running correctly with:

```bash
$ mailchain version
Version: v0.0.12
```

You should see the version number of the application.

## Prerequisites

Mailchain depends on external resources, an [Ethereum JSON-RPC Endpoint](https://github.com/ethereum/wiki/wiki/JSON-RPC) for sending transactions and [Amazon S3](https://aws.amazon.com/s3/) to store sent messages.

### Ethereum JSON-RPC Endpoint

A JSON-RPC Endpoint is required to send transactions, a node is required for each network you want to send transactions on. There are different options for getting access to a JSON-RPC endpoint, we recommend using [Infura](https://infura.io/), its a managed service and there is no cost.

* [Infura](https://infura.io/) - Sign up for an account and create an endpoint. Each endpoint has a unique URL.
* [Go Ethereum](https://geth.ethereum.org/) - [Install](https://geth.ethereum.org/install-and-build/Installing-Geth) and run a node. You can enable the JSON-RPC Endpoint and [obtain](https://github.com/ethereum/wiki/wiki/JSON-RPC#json-rpc-endpoint) the URL.
* [Parity](https://www.parity.io/) - [Install](https://www.parity.io/ethereum/#download) and enable the JSON-RPC Endpoint and [obtain](https://wiki.parity.io/JSONRPC) the URL.

In each case the URL is supplied when [initializing](getting-started.md#initialize) the Mailchain application.

{% hint style="info" %}
We are working to remove the requirement of having access to a JSON-RPC Endpoint, you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/120). Subscribe to notifications to track our progress.
{% endhint %}

### Amazon S3

Mailchain will support multiple sent storage options. Currently Amazon S3 is the only supported storage. Amazon S3 can be configure either through the console, via the CLI, or with CloudFormation. We recommend using CloudFormation, to make this easier we have supplied a [template](https://github.com/mailchain/sent-storage-s3) you can run in your account. The easiest way to create this resource is by clicking on the launch stack icon below.

[![Launch Stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=mailchain-sent-storage&templateURL=https://s3.amazonaws.com/mailchain-sent-storage-s3-cloudformation-template/output.yaml)

{% hint style="info" %}
We are working to remove the requirement of having to configure Amazon S3 for sent storage , you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/119). Subscribe to notifications to track our progress.
{% endhint %}

We are working to remove the requirement of having to configure Amazon S3 for sent storage , you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/119). Subscribe to notifications to track our progress.

{% hint style="info" %}
We are working to remove the requirement of having to configure Amazon S3 for sent storage , you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/119). Subscribe to notifications to track our progress.
{% endhint %}

You are now ready to [initialize](getting-started.md#initialize) the application.

## Initialize

When using Mailchain for the first time you need to initialize the application.

{% hint style="info" %}
Ensure that you have setup the [prerequisites](getting-started.md#prerequisites) to run Mailchain.
{% endhint %}

Simply run:

```bash
mailchain init
```

Follow the instructions inserting the settings from the prerequisites. If you made a mistake, will need to remove the .mailchain.yaml file. You can simple run `mailchain init` again and it will give you the option to remove the current file and start over.

## Add Account



To send and receive messages with Mailchain you will need to add an account. To do this you will need your private key.

```bash
mailchain account add --chain=ethereum --private-key=[PRIVATE-KEY-VALUE]
```

* `--chain` is the chain which the key is added to. Currently supported `[ethereum]`.
* `--private-key` the private key value which should be added. The public key and account will be calculated.
* `--passphrase` is can be optionally supplied in the command line or at the prompt when the application starts.

{% hint style="info" %}
_Mailchain stores your private key in an encrypted format, a passphrase is required._ Enter a non-guessable passphrase, and again to confirm it. You must remember your password to decrypt the key later.
{% endhint %}

{% hint style="danger" %}
You should never expose your private keys to an entity you don't trust. Mailchain stores your private key locally, in an encrypted format. Your private keys are never sent anywhere. They are only used to decrypt messages data, and sign transactions.
{% endhint %}



