---
description: How to get started sending a Mailchain test message on a testnet
---

# Sending Ethereum Testnet Messages

### Ethereum Testnets

To send testnet messages using Mailchain, you will need an Ethereum address with a small balance \(around 0.0007 Ether\).

Ethereum addresses are valid across the Ethereum mainnet and testnets, so it's best to create a **new address for development purposes only**. This way, if your private key gets exposed, only test ETH can get stolen.

#### 1. Create an Ethereum Address for Testing/ Development

To create a new Ethereum address, we recommend using either [MyCrypto](https://mycrypto.com/generate) or [Metamask](https://metamask.io/) \(which comes built into [Brave Browser](https://brave.com/)\).

{% hint style="danger" %}
Please take the time to write everything down that enter into your computer.  
At the least, you'll need to record a seed phrase \(or private key\) and password.
{% endhint %}

#### 2. Get Some Test ETH

**Metamask**

If you are using Metamask, you can switch networks in the Metamsk interface and go to [https://faucet.metamask.io/](https://faucet.metamask.io/)

**MyCrypto or Other Wallet Software**

You can head to one of the following faucets and follow the instructions to be sent some test ether.

| Network | Faucets \(all working at the time of writing\) |
| :--- | :--- |
| Mainnet | N/A |
| Ropsten | [https://faucet.ropsten.be/](https://faucet.ropsten.be/) |
| Goerli | [https://faucet.goerli.mudit.blog/](https://faucet.goerli.mudit.blog/) |
| Kovan | [https://faucet.kovan.network/](https://faucet.kovan.network/) |
| Rinkerby | [https://www.rinkeby.io/\#faucet](https://www.rinkeby.io/#faucet) |

#### 3. Install Mailchain

Follow the docs at [Getting Started](../getting-started.md) and add your private key for the test/dev ethereum address you created in [step 1](sending-testnet-messages.md#1-create-an-ethereum-address-for-testing-development).

#### 4. Load Your Mailchain Inbox

With your Mailchain [client running locally](../advanced-configuration/setting-up.md#serve), head to the Mailchain Inbox \([https://inbox.mailchain.xyz](https://inbox.mailchain.xyz)\).

#### 5. Switch To A Testnet

In the Mailchain Inbox, [switch to the testnet ](../mailchain-web-inbox/configuring-the-web-interface.md#changing-the-network)that you want to send a message on \(and have a balance on\).

#### 6. Compose and Send a Message

{% hint style="info" %}
Because you have not yet sent any transactions from this ethereum address on this network, Mailchain won't be able to be able to determine your public key.
{% endhint %}

_If this is the first message or transaction you are sending on this testnet:_

Click "COMPOSE" in the Inbox interface and send a message to an ethereum address which has already sent a transaction, e.g. the Mailchain Developer address: 0x4ad2b251246aafc2f3bdf3b690de3bf906622c51.

If you have sent a message or transaction on this testnet, you can receive messages from other developers, send messages to yourself, either from the same address or another development address.

{% hint style="success" %}
Top tip: Because Mailchain supports ENS, you can configure an easy, human readable name for your development address on the testnet you are working on. This makes it easier to keep track when switching between different addresses.
{% endhint %}



