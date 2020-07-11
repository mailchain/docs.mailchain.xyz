# Advanced Storage Configuration

### Configuring Mailchain to Use Your Own Sent Storage Location

Mailchain will supports multiple sent storage options:

1. \*\*\*\*[**Mailchain**](advanced-storage-configuration.md#mailchain) \(encrypted sent store, managed by Mailchain on Amazon S3\)
2. \*\*\*\*[**Amazon S3**](advanced-storage-configuration.md#amazon-s3) \(encrypted sent store, in your own Amazon S3 account\)
3. \*\*\*\*[**IPFS**](advanced-storage-configuration.md#ipfs) \(encrypted sent store, pinned indefinitely, using [Pinata](https://pinata.cloud)\)

### Mailchain \(Default\)

#### **Setting Up Mailchain-Managed Storage**

For convenience, Mailchain provides a storage endpoint for messages. This is configured by default.

If you need to re-apply the configuration, you can update the `mailchain.yaml` configuration file with:

```yaml
sentstore:
  kind: "mailchain"
```

### Amazon S3

#### Setting Up Amazon S3

Amazon S3 can be configured either through the console, via the CLI, or with CloudFormation. We recommend using CloudFormation, to make this easier we have supplied a [template](https://github.com/mailchain/sent-storage-s3) you can run in your account. The easiest way to create this resource is by clicking on the launch stack icon below.

[![Launch Stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=mailchain-sent-storage&templateURL=https://s3.amazonaws.com/mailchain-sent-storage-s3-cloudformation-template/output.yaml)

You can now update the `mailchain.yaml` configuration file with your S3 details:

```yaml
sentstore:
  kind: "s3"
  s3:
   accessKeyId: "YOUR-S3-ACCESS-KEY"
   bucket: "YOUR-S3-BUCKET"
   region: "YOUR-S3-REGION"
   secretAccessKey: "YOUR-S3-ACCESS-SECRET"
```

### IPFS

#### Setting Up IPFS using Pinata

Mailchain supports IPFS using Pinata \([https://pinata.cloud](https://pinata.cloud)\). It's easy to get started, simply sign up \(and confirm your email address\), then get your API key and API secret to use Pinata as the sent store.

You can now update the `mailchain.yaml` configuration file with your Pinata details:

```yaml
sentstore:
  kind: "pinata"
  pinata:
    api-key: "YOUR-PINATA-API-KEY"
    api-secret: "YOUR-PINATA-API-SECRET"
```

