---
description: Instructions on how to upgrade to the latest version of Mailchain
---

# Upgrading

## What Version of Mailchain Am I Running?

To check which version of Mailchain you are running, use the `mailchain version` command. For example:\`

```bash
$ mailchain version
Version: v0.0.36
```

The latest release version can be seen on the [Mailchain releases page on Github](https://github.com/mailchain/mailchain/releases/latest).

## Upgrade on a Mac via Homebrew

If you used [Homebrew](https://brew.sh/) to install Mailchain, you can easily upgrade by running:

```bash
brew upgrade mailchain
```

#### Checking if Mailchain was installed using Homebrew

You can check if Mailchain was installed with Homebrew by running:

```bash
brew list mailchain
```

Installed: `/usr/local/Cellar/mailchain/X.Y.Z/bin/mailchain`

Not installed: `Error: No such keg: /usr/local/Cellar/mailchain`

## Quick Upgrade \(Linux and Windows\)

To upgrade Mailchain suing the installation scripts, run the following command to download and upgrade the application on your local machine.

```bash
curl -sL https://run.mailchain.xyz/install.sh | sh
```

## Manual Upgrade

To choose where to store the application, you can install mailchain manually.

### Download the latest release

Download the application directly via the [Mailchain releases](https://github.com/mailchain/mailchain/releases/latest) page. Save it to the directory you initially saved mailchain to \(we recommended you save it in your home directory: `~/.mailchain/bin`\).

#### Checking where Mailchain is saved to:

To check where Mailchain was saved to, run the following command in Terminal:

```bash
which mailchain
```

## 



