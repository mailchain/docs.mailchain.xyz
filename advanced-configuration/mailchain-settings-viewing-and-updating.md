# Mailchain Settings: Viewing and Updating

By default, Mailchain comes preconfigured with some default values to make it easier to get started.

To configure your own values, for example, adding your API Key for Etherscan to retrieve your messages, you can edit the config \(by default located in `~/.mailchain/.mailchain.yaml` \)

By default, `mailchain.yaml` only has a few lines of config, e.g.

```text
server:
  cors:
    disabled: false
  port: 8080
version: 0.0.65
```

Each value you add to the config overrides the default value. To view the current values, run the following command:

```text
mailchain settings view
```

It will show the default values with `#` in front. 

![Mailchain default settings](../.gitbook/assets/image%20%2814%29.png)

To edit the values, for example, adding an Etherscan.io API Key \(available [here](https://etherscan.io/myapikey)\) to be able to poll their API and check for new messages on Ethereum Mainnet, add the following to you config file:

```text
server:
  cors:
    disabled: false
  port: 8080
protocols:
  ethereum:
    networks:
      mainnet:
        public-key-finder: "etherscan"
        receiver: "etherscan"
public-key-finders:
  etherscan:
    api-key: "<YOUR-ETHERSCAN_API_KEY>"
receivers:
  etherscan:
    api-key: "<YOUR-ETHERSCAN_API_KEY>"
```

Now if you run the `mailchain settings view` command again, you will see that the config shows in the output without the `#` before the line:

![](../.gitbook/assets/image%20%2812%29.png)

![](../.gitbook/assets/image%20%2811%29.png)

![](../.gitbook/assets/image%20%2810%29.png)

Now, when you run `mailchain serve`, the Mailchain API client will be using the values you configured.

To revert to defaults, simply remove the value from the config file.

