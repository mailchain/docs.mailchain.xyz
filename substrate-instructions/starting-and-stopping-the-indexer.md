# Starting and Stopping the Indexer

Ensure you have [installed the indexer](installing-the-indexer.md).

### Starting the Indexer

To start the indexer container, run:

```bash
docker-compose -f ~/docker/mailchain/docker-compose.substrate.yml up --build
```

NOTE: You may need to adjust the path to the location you downloaded your docker-compose file.

### Stopping the Indexer

To gracefully stop the receiver, press `Ctrl+C`.

