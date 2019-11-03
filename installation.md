---
description: Follow the steps below to install Mailchain...
---

# Installation

## Quick Install \(Mac\)

To install Mailchain for the first time, we recommend using [Homebrew](https://brew.sh/) to download, install and manage the application on your local machine.

First we need to tap mailchain repository to the list of formulae that brew tracks using

```bash
brew tap mailchain/tap
```

Once you have done this, you can install mailchain using 
```bash
brew install mailchain
```

## Quick Install \(Linux and Windows\)

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

You are now ready to [initialize](setting-up.md) the application.

