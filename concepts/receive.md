# Receive

Messages are received by querying transactions sent to an address via the address index. This is then filtered for transactions containing a Mailchain envelope. [Envelopes](../reference/programmable-envelopes.md) are then decoded to extract message contents.

Because each blockchain protocol may have differences in the way data and transactions are handled, Mailchain uses a standard format plus any protocol specifics.

### Address Index

To see all recipient messages, a list of all transactions sent to that recipient is required. Not all blockchain protocols have an address index as part of the core implementation. If this does not exist, a third party or custom index can be used to build the index.

### Filtering

Once the address index returns all of the transactions received by an address, they need to be filtered to extract transactions that contain Mailchain envelopes in transaction data field. The expected format is:

```text
[protocol-prefix]+[mailchain-prefix]+[envelope]
```

The filtering removes the prefix and searches for a `mailchain-prefix`.

### Decoding Envelope

Programmable envelopes contain message information fields: URL, IntegrityHash, and ContentsHash. This information allows the recipient to download, validate, and verify the message. Decoding the envelope removes the `[protocol-prefix]`and `[mailchain-prefix]` to leave the `[envelope]` bytes for processing the message. 





