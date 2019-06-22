---
title: Dependencies
weight: 4
menu: true
---

Mailchain depends on two external resources, an [Ethereum JSON-RPC Endpoint](https://github.com/ethereum/wiki/wiki/JSON-RPC) for sending transactions and [Amazon S3](https://aws.amazon.com/s3/) to store sent messages.

## Quick Configuration
Mailchain works without configuring any 3rd party dependencies. You can simply [initialize](/app-init) the application.

___
## Advanced Configuration
Mailchain enables you to choose how you send messages to a blockchain and where those messages are stored. For example, you can use a 3rd party API or your own node to send the message and store them in a location you control.

### Ethereum JSON-RPC Endpoint

A JSON-RPC Endpoint is required to send transactions, a node is required for each network you want to send transactions on. There are different options for getting access to a JSON-RPC endpoint, we recommend using [Infura](https://infura.io/), its a managed service and there is no cost.

+ [Infura](https://infura.io/) - Sign up for an account and create an endpoint. Each endpoint has a unique URL.
+ [Go Ethereum](https://geth.ethereum.org/) - [Install](https://geth.ethereum.org/install-and-build/Installing-Geth) and run a node. You can enable the JSON-RPC Endpoint and [obtain](https://github.com/ethereum/wiki/wiki/JSON-RPC#json-rpc-endpoint) the URL.
+ [Parity](https://www.parity.io/) - [Install](https://www.parity.io/ethereum/#download) and enable the JSON-RPC Endpoint and [obtain](https://wiki.parity.io/JSONRPC) the URL.

In each case the URL is supplied when [initializing](/app-init) the Mailchain application.

> **ATTENTION**: We are working to remove the requirement of having access to a JSON-RPC Endpoint, you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/120). Subscribe to notifications to track our progress.

