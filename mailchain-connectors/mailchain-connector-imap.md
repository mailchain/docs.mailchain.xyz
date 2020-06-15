---
description: >-
  The Mailchain Connector for IMAP makes it possible to receive Mailchain
  messages in your email inbox...
---

# Mailchain Connector for IMAP

The Mailchain Connector for IMAP makes it possible to receive Mailchain messages in your email inbox \(i.e. your webmail, desktop or phone mail application\).

It connects to the Mailchain API, converts messages to emails, then uploads them to your chosen IMAP mailbox.

### Installation

#### Prerequisites

You need to have already installed:

1. The Mailchain API client \([https://docs.mailchain.xyz/installation](https://docs.mailchain.xyz/installation)\)
2. Ruby \(we suggest using [RVM](https://rvm.io/)\)

#### Installation and Setup

Install `mailchain_connector_imap` by running:

```bash
  gem install mailchain_connector_imap
```

Next, if running mailchain\_connector\_imap for the first time, or to change the configuration, run:

```bash
  mailchain_connector_imap --configure
```

This will walk you through the configuration options \(for more information on details, see [Configuration Details](mailchain-connector-imap.md#configuration-details) below\).

#### Running the Mailchain Connector for IMAP

Once installed and configured, run the connector. It will prompt you to enter your IMAP \(email\) password so it can connect to the IMAP server:

```bash
  mailchain_connector_imap
```

### Configuration Details

The `mailchain_connector_imap` configuration is stored at `~/.mailchain_connector/imap/config.json`.

The wizard steps through the following options:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Question</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>IMAP Settings:</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">IMAP server</td>
      <td style="text-align:left">
        <p>The hostname of the IMAP server.</p>
        <p>e.g. imap.example.com</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">IMAP username</td>
      <td style="text-align:left">
        <p>Your IMAP username, usually your email address.</p>
        <p>e.g. tim@example.com</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">IMAP Port</td>
      <td style="text-align:left">
        <p>The port that the IMAP server is listening on.</p>
        <p>e.g. IMAP = 143 or IMAP SSL = 993</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Use SSL</td>
      <td style="text-align:left">Recommended if your IMAP server supports this.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Mailchain Settings:</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Mailchain client hostname</td>
      <td style="text-align:left">The hostname or IP address where the Mailchain client is running. If you
        are running the client on your local machine, this is likely to be 127.0.0.1.
        <br
        />e.g. 127.0.0.1 or mailchain.example.com</td>
    </tr>
    <tr>
      <td style="text-align:left">Use HTTPS (SSL)</td>
      <td style="text-align:left">
        <p>If the Mailchain client is hosted, it will likely connect over https.</p>
        <p>NOTE: When running locally, the Mailchain client does not use HTTPS.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Mailchain client port</td>
      <td style="text-align:left">
        <p>The port that the Mailchain client is listening on.</p>
        <p>If you are running the client on your local machine with configuration
          defaults, this is likely to be 8080.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Folder Structure for IMAP</td>
      <td style="text-align:left">
        <p>The structure of the folders in IMAP can be either:</p>
        <p>Protocol&gt;Network&gt;Address</p>
        <p>or</p>
        <p>Address&gt;Protocol&gt;Network</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mainnet</code> messages delivered Inbox folder</td>
      <td style="text-align:left">Because most IMAP servers will only alert a user when a new message arrives
        in the Inbox, rather than other folders, some users prefer to receive `mainnet`
        messages in their regular Inbox folder.</td>
    </tr>
    <tr>
      <td style="text-align:left">Message check interval</td>
      <td style="text-align:left">Configured in seconds. Minimum interval is 60 seconds.
        <br />e.g. 300 = 5 minutes</td>
    </tr>
  </tbody>
</table>

_Sample configuration file:_

```text
{
  "imap": {
    "server": "imap.example.com",
    "username": "tim@example.com",
    "port": "993",
    "ssl": true
  },
  "mailchain": {
    "hostname": "127.0.0.1",
    "ssl": false,
    "port": "8080",
    "folders": "by_network",
    "mainnet_to_inbox": true,
    "interval": "300"
  }
}
```

### FAQs

**Can I connect my regular email account using the Mailchain Connector to receive Mailchain messages?**  
Yes. The Mailchain Connector for IMAP works with any IMAP-supported email account.  
NOTE: You may want to create a new email account with the sole purpose of receiving Mailchain messages to achieve separation between messages.

**Can I use the Mailchain Connector for IMAP with Gmail?**  
Yes. We recommend you follow the instructions to create an [App Password](https://support.google.com/accounts/answer/185833?hl=en) to sign into your Gmail account, then configure your IMAP settings as [recommended by Gmail](https://support.google.com/mail/answer/7126229?hl=en-GB). 

**Can I use the Mailchain Connector for IMAP with my own IMAP server?**  
Yes. Simply configure the IMAP settings according to the configuration instructions.

**Can I store my IMAP password in the Mailchain Connector for IMAP configuration?**  
No. We prefer you enter it at runtime so your email credentials are not stored on the local machine.

**Can I view Mailchain messages in email client on my desktop \(e.g. Outlook or Mail\), iPhone, Android, or other smartphone?**  
Yes. By using the Mailchain Connector for IMAP to transfer your Mailchain messages to an IMAP email account, you can connect your email client to that IMAP email account to receive the messages in the same way as you would receive regular email. 

**Are the Mailchain messages still encrypted when they are sent to my IMAP server?**  
No. The Mailchain client decrypts messages so they can be converted into regular emails before being transferred to the IMAP server.

**Will my email provider be able to read my Mailchain messages?**  
Because the Mailchain messages are converted to emails before being stored on the IMAP server, your email provider will have the same visibility of the your Mailchain messages as any other email in your inbox.  
NOTE: Greater privacy can be achieved by running your own email server.

**Can I search the Mailchain messages in my email inbox?**  
Yes. The Mailchain messages in your email inbox will be searchable in the same way as any other email might be.

**Can I reply to messages from my email client?**  
No. In order to reply to Mailchain messages, an SMTP connector would be required. This is on the roadmap.

**Where can I find the log file for the Mailchain Connector for IMAP?**  
You can find the logs here: `~/.mailchain_connector/imap/mailchain_connector_imap.log`

**How do I uninstall the Mailchain Connector for IMAP?**  
To uninstall the Mailchain Connector for IMAP, run`gem uninstall mailchain_connector_imap`  
Next, delete the folder `~/.mailchain_connector/imap/`



