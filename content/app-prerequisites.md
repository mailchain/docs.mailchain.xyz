---
title: Prerequisites
weight: 4
menu: true
---

Mailchain depends on two external resources, an [Ethereum JSON-RPC Endpoint](https://github.com/ethereum/wiki/wiki/JSON-RPC) for sending transactions and [Amazon S3](https://aws.amazon.com/s3/) to store sent messages.

## Ethereum JSON-RPC Endpoint

A JSON-RPC Endpoint is required to send transactions, a node is required for each network you want to send transactions on. There are different options for getting access to a JSON-RPC endpoint, we recommend using [Infura](https://infura.io/), its a managed service and there is no cost.

+ [Infura](https://infura.io/) - Sign up for an account and create an endpoint. Each endpoint has a unique URL.
+ [Go Ethereum](https://geth.ethereum.org/) - [Install](https://geth.ethereum.org/install-and-build/Installing-Geth) and run a node. You can enable the JSON-RPC Endpoint and [obtain](https://github.com/ethereum/wiki/wiki/JSON-RPC#json-rpc-endpoint) the URL.
+ [Parity](https://www.parity.io/) - [Install](https://www.parity.io/ethereum/#download) and enable the JSON-RPC Endpoint and [obtain](https://wiki.parity.io/JSONRPC) the URL.

In each case the URL is supplied when [initializing](/app-init) the Mailchain application.

> **ATTENTION**: We are working to remove the requirement of having access to a JSON-RPC Endpoint, you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/120). Subscribe to notifications to track our progress.

## Amazon S3

Mailchain will support multiple sent storage options. Currently Amazon S3 is the only supported storage. Amazon S3 can be configure either through the console, via the CLI, or with CloudFormation. We recommend using CloudFormation, to make this easier we have supplied a [template](https://github.com/mailchain/sent-storage-s3) you can run in your account. The easiest way to create this resource if by clicking on the launch stack icon below.

[![Launch Stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=mailchain-sent-storage&templateURL=https://s3.amazonaws.com/mailchain-sent-storage-s3-cloudformation-template/output.yaml)

> **ATTENTION**: We are working to remove the requirement of having to configure Amazon S3 for sent storage , you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/119). Subscribe to notifications to track our progress.

You are now ready to [initialize](/app-init) the application.