---
title: Install
weight: 3
menu: true
---

If this is your first time running Mailchain, you’ll need to download the application onto your local machine. You’ll use this application to interact with the blockchain to send and receive messages.

Installing Mailchain is fast and easy.

To install the application, run:

```sh
curl -sL https://run.mailchain.xyz/install | sh
```

Alternatively, you can download the application directly via the [Mailchain releases](https://github.com/mailchain/mailchain/releases/latest) page.

Next, add mailchain to your path with:

```sh
export PATH=$PATH:$HOME/.mailchain/bin
```

Verify the application is installed and running correctly with:

```sh
$ mailchain version
Version: v0.0.4
```

You should see the version number of the application.