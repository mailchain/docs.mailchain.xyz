# Installing, Starting & Stopping The Indexer

### Installation

The transaction indexer comes as a docker cluster which runs locally.

#### Prerequisites

[Docker](https://www.docker.com/) should be installed and running.

Clone the Mailchain repository to your `.mailchain/mailchain` folder:

```text
git clone https://github.com/mailchain/mailchain.git ~/.mailchain/mailchain
cd ~/.mailchain/mailchain
```

### Starting the Indexer

The indexer is preconfigured for 3 networks:

| Network | Command |
| :--- | :--- |
| Edgeware Mainnet | `make edgeware-mainnet` |
| Edgeware Testnet \(beresheet\) | `make edgeware-beresheet` |
| Edgeware Local \(development\) | `make edgeware-local` |

Select the network and run the appropriate make command \(e.g. `make edgeware-mainnet`\). This will download or update the required docker containers.

NOTE: If working in local mode, you can access the preconfigured development accounts [here](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/accounts) if you need to transfer a balance to accounts you configured in [Setting Up &gt; Add Account](../ethereum-instructions/setting-up.md#add-account).

If successful, the output will be similar to the following:

```text
Creating network "mailchain_default" with the default driver
Pulling database (postgres:)...
latest: Pulling from library/postgres
bf5952930446: Downloading [===============>                                   ]  8.399MB/27.09MB
...
Creating mailchain_database_1 ... done
Creating mailchain_receiver_1                  ... done
Creating mailchain_indexer-migration_1         ... done
Creating mailchain_indexer-substrate-mainnet_1 ... done
...
indexer-substrate_1  | 2020/09/27 19:19:51 Connecting to ws://mainnet1.edgewa.re:9944...
receiver_1           | [negroni] listening on :8080
indexer-substrate_1  | block number:  3191664
indexer-substrate_1  | block hash:  0x81c694ba6973213905a8beaa8f8b69db395fb060606411d19c4f3b575c5f9b4c
indexer-substrate_1  | next block number:  3191665
indexer-substrate_1  | block number:  3191665
```

### Stopping the Indexer

To gracefully stop the indexer, press `Ctrl+C`.

### 

