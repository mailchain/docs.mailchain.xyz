---
title: Install
weight: 3
menu: true
---

## Quick Install  
To install Mailchain for the first time, run the following command to download and install the application on your local machine.


```sh
curl -sL https://run.mailchain.xyz/install.sh | sh
```

## Advanced Manual Install
To choose where to store the application, you can install mailchain manually.

### 1. Download the application
Download the application directly via the [Mailchain releases](https://github.com/mailchain/mailchain/releases/latest) page. We recommend you save it in your home directory: `~/.mailchain/bin`

### 2. Export the application path
Next, add mailchain to your path with:

```sh
export PATH=$PATH:$HOME/.mailchain/bin
```

Verify the application is installed and running correctly with: `mailchain version`. For example:`

```sh
$ mailchain version
Version: v0.0.11
```

Next, if the application is working as expected, you’ll want to add the path to `~/.profile`, `.zshrc`, or `~/.bash_profile`, depending on which shell you use.

To determine the shell you use, run `echo $SHELL`. For example, if using zsh, as shown below:

```sh
$ echo $SHELL
```


Shell output | Command to export the path to the shell profile
- | -
/bin/zsh | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.zshrc`
/bin/bash | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.bashrc`
/bin/ksh | `echo 'export PATH=$PATH:$HOME/.mailchain/bin' >> ~/.kshrc`
