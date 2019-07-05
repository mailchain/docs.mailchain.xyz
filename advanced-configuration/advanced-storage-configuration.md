# Advanced Storage Configuration

### Configuring Mailchain to Use Your Own Sent Storage Location

Mailchain will support multiple sent storage options.

Currently Amazon S3 is the only supported sent storage.

#### Setting Up Amazon S3

Amazon S3 can be configure either through the console, via the CLI, or with CloudFormation. We recommend using CloudFormation, to make this easier we have supplied a [template](https://github.com/mailchain/sent-storage-s3) you can run in your account. The easiest way to create this resource is by clicking on the launch stack icon below.

[![Launch Stack](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=mailchain-sent-storage&templateURL=https://s3.amazonaws.com/mailchain-sent-storage-s3-cloudformation-template/output.yaml)

> **ATTENTION**: We are working to remove the requirement of having to configure Amazon S3 for sent storage , you can track the progress at [this issue](https://github.com/mailchain/mailchain/issues/119). Subscribe to notifications to track our progress.

You are now ready to [initialize](/app-init) the application.

