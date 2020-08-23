---
description: >-
  The Mailchain Substrate Transaction Indexer makes it possible to listen for
  Mailchain messages on Substrate chains where the contracts module is
  configured for configured account addresses
---

# Substrate Transaction Indexer

Substrate does not natively support an address index or similar functionality that identifies all transactions sent to or from a specific address.

The Mailchain Substrate Transaction Indexer makes it possible to listen for Mailchain messages in Substrate extrinsics for configured accounts. The Mailchain API can then retrieve mailchain messages from the indexer for those configured accounts.

The latest version of the substrate indexer can be found here: [https://github.com/mailchain/mailchain/blob/master/docker-compose.substrate.yml](https://github.com/mailchain/mailchain/blob/master/docker-compose.substrate.yml)

