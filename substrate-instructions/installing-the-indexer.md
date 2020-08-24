# Installing the Indexer

### Installation

The transaction indexer comes as a docker cluster which runs locally.

#### Prerequisites

You need to have already installed:

1. [Docker](https://www.docker.com/)

#### Installation and Setup

To obtain the latest docker container download the docker-compose file from the Mailchain repository: [https://github.com/mailchain/mailchain/blob/master/docker-compose.substrate.yml](https://github.com/mailchain/mailchain/blob/master/docker-compose.substrate.yml). Save the [raw file](https://raw.githubusercontent.com/mailchain/mailchain/master/docker-compose.substrate.yml) in your preferred location for docker-compose files.

For this example the container file is stored as `~/docker/mailchain/docker-compose.substrate.yml`using the command:

```text
mkdir -p ~/docker/mailchain
curl https://raw.githubusercontent.com/mailchain/mailchain/master/docker-compose.substrate.yml >> ~/docker/mailchain/docker-compose.substrate.yml
```

Next, open the file in your editor and update any default values \(e.g. network, ports or passwords\). For this example, we will keep the default Edgeware Mainnet configuration.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Service</th>
      <th style="text-align:left">Image</th>
      <th style="text-align:left">Configuration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>database</code>
      </td>
      <td style="text-align:left">postgres</td>
      <td style="text-align:left">The postgres image configuration</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>indexer-migration</code>
      </td>
      <td style="text-align:left">mailchain/indexer</td>
      <td style="text-align:left">Configuration for the mailchain/indexer</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>indexer-substrate-mainnet</code>
      </td>
      <td style="text-align:left">mailchain/indexer</td>
      <td style="text-align:left">
        <p>Configuration for the:</p>
        <ul>
          <li>RPC endpoint to use</li>
          <li>Starting block</li>
          <li>Database image access</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>receiver</code>
      </td>
      <td style="text-align:left">mailchain/receiver</td>
      <td style="text-align:left">Configuration for the mailchain/receiver</td>
    </tr>
  </tbody>
</table>

Once you have updated your configuration, run the following to start the indexer container:

```bash
docker-compose -f ~/docker/mailchain/docker-compose.substrate.yml up --build --no-start
```

NOTE: You may need to adjust the path to the location you downloaded your docker-compose file.

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
```

### 

