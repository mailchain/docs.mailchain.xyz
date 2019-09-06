# Read

Message metadata is extracted after [decoding the contents of an envelope](receive.md#read-envelope). This provides the URL, IntegrityHash, and ContentsHash. With this metadata the message can be [downloaded](read.md#download), [decrypted](read.md#decrypt), and [decoded](read.md#decode).

### Download

The envelope contains a [URL](../reference/programmable-envelopes.md#url) field which specifies the location of a message which is accessible to the recipient to download.

Envelopes have an optional [IntegrityHash](../reference/programmable-envelopes.md#integrityhash) which returns a hash represented as a byte array. If this field is available, the hash must be used to validate the contents of the downloaded message before proceeding. This ensure the contents of the message has not been altered.

{% hint style="info" %}
Contents of the message cannot be changed after it has been sent without invalidating the IntegrityHash or ContentsHash. Downloaded message contents can be cached indefinitely.
{% endhint %}

### Decrypt

If appropriate, to ensure a message can only be read by the recipient it is [encrypted with the recipient public key](send.md#content-encryption). Once the contents have been [downloaded and validated](read.md#download) they can be decrypted. The first byte of the encrypted contents describes the encryption method used. This indicates which cipher is required for decryption. After the message contents have been decrypted successfully, it can be verified by comparing the [ContentsHash](../reference/programmable-envelopes.md#contentshash) contained in the envelope with a hash of the decrypted contents. The default hash function is `SHA3-256`.

{% hint style="danger" %}
The ContentsHash provides a cryptographically secure mechanism to ensure the contents of the message are as the sender intended. If the hashes do not match the contents should not be trusted and discarded.
{% endhint %}

### Decode

Mailchain message contents can be encoded with different methods depending on the type and contents. To ensure that the correct method is used to decode the message inspect the `Content-Type` and `Content-Transfer-Encoding` message headers that were set when [preparing to send](send.md#message-preparation) the message.

Once decoded, the message fields \(headers, subject, body, etc.\) can be extracted and displayed to a user through an interface.

