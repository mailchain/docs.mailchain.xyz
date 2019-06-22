---
title: Initialize
weight: 5
menu: true
---


When using Mailchain for the first time you need to initialize the application.

Run:

```sh
mailchain init
```

Follow the instructions to select the network and choose a sender protocol.

If you need to configure your own endpoint for sending transactions, see *Advanced Configuration* under [prerequisites](/app-prerequisites) to obtain the correct url.

Otherwise, for simplicity, we suggest using the following for the corresponding network:

Network | Endpoint
- | -
Mainnet | https://mainnet.infura.io
Kovan  | https://kovan.infura.io
Rinkeby  | https://rinkeby.infura.io
Ropsten  | https://ropsten.infura.io
Goerli  | https://goerli.infura.io


 ##### Additional networks
 Note: You can configure additional networks after initialization.

##### Made a mistake?
inserting the settings from the prerequisites. If you made a mistake, will need to remove the .mailchain.yaml file. You can simple run `mailchain init` again and it will give you the option to remove the current file and start over.