# Programmable Envelopes

Programmable envelopes contain predefined fields to allow different types of messages to be sent according to specific use case requirements. Mailchain is flexible and extensible, adding a messaging layer to blockchain protocols, supporting different types of messages to be sent. Blockchain protocols typically allow sending `data` as a byte array, which is efficient but not descriptive. Programmable Envelopes allow descriptive implementations of messaging use cases that can be encoded to a byte array.

Each envelope is implemented as code, describing the encoding method, fields, and interface functions. 

Programmable Envelopes are preferred over adding optional fields. They remove some of the complexity, the need for additional documentation, are extensible in a modular sense, and create an improved developer experience.

{% hint style="info" %}
Backwards and forwards compatibility can be achieved by never modifying an envelope after deployment.
{% endhint %}

## Envelopes

### 0x00 - Reserved for unset value

Zero value is reserved to identify that it has not been set and should be treated like an unset envelope identifier. 

### 0x01 - Private Message Stored with MLI

The Private Message Stored with MLI \(Message Location Identifier\) is optimized for secure, verifiable messaging with minimal bytes, [URL](programmable-envelopes.md#url) and [ContentsHash](programmable-envelopes.md#contentshash) are encrypted with a publicly verified [IntegrityHash](programmable-envelopes.md#integrityhash). 0x01 uses [MLI](types.md#message-location-identifier) to reduce the bytes needed to store the [URL](programmable-envelopes.md#url), the [IntegrityHash](programmable-envelopes.md#integrityhash) is optional reducing the required number of bytes.

#### Encoding

[Protocol buffers](https://developers.google.com/protocol-buffers/) are used to define the structure of this message. This is the `proto3` spec. 

```text
// Use hosted location where the decryptedhash is the same as the location. Location, decrypted hash are encrypted so only receipient can location and verify the message.
message ZeroX01 {
    bytes UIBEncryptedLocationHash = 1;
    bytes encryptedHash = 2;
}
```

**Fields**

| **Name** | Type | Notes |
| :--- | :--- | :--- |
| UIBEncryptedLocationHash | bytes | _Required_ - Bytes are stored are represented with [UInt64Bytes](types.md#uint-64-bytes). |
| encryptedHash | bytes | _Optional_ - Bytes of hash |

### 0x02 - Private Message Stored on IPFS

The Private Message Stored on [IPFS](https://ipfs.io/) \(InterPlanetary File System\) is optimized for secure, verifiable messaging with minimal bytes, [URL](programmable-envelopes.md#url) and [IntegrityHash](programmable-envelopes.md#integrityhash) are encrypted with a verified [ContentsHash](programmable-envelopes.md#contentshash). 0x02 uses an `ipfs://` URL, the [ContentsHash](programmable-envelopes.md#contentshash) is required.

#### Encoding

[Protocol buffers](https://developers.google.com/protocol-buffers/) are used to define the structure of this message. This is the `proto3` spec. 

```text
// Use hosted location where the encrypted hash is the same as the location. Location and decrypted hash are encrypted so only receipient can location and verify the message.
message ZeroX02 {
    bytes UIBEncryptedLocationHash = 1;
    bytes decryptedHash = 2;
}
```

**Fields**

| **Name** | Type | Notes |
| :--- | :--- | :--- |
| UIBEncryptedLocationHash | bytes | _Required_ - Bytes are stored are represented with [UInt64Bytes](types.md#uint-64-bytes). |
| decryptedHash | bytes | _Required_ - Bytes of hash |

#### 0x50 - Alpha

## Implementation

### Encoding

The first byte will describe the envelope implementation and encoding method used.

| Byte Value | Notes |
| :--- | :--- |
| `0x00` | **Reserved** for unset value |
| `0x01` | [Private message stored with MLI](programmable-envelopes.md#0x01-private-message-stored-with-mli) |
| `0x50` | [Alpha envelope](programmable-envelopes.md#0x50-alpha) |
| `0xFF` | **Reserved** to extend beyond 255 envelope definitions |

{% hint style="info" %}
While [Protocol buffers](https://developers.google.com/protocol-buffers/) are used by the first implemented envelopes, this is not a requirement. Each envelope describes it encoding method in the definition.
{% endhint %}

### Interface

Each envelope is required to implement the data interface. The interface enables each different envelope to define its implementation of the methods, this allows for different combinations of fields or logic to return a valid response for each of these methods. 

This interface is defined as:

```go
type Data interface {
	URL(decrypter cipher.Decrypter) (url *url.URL, err error)
	IntegrityHash(decrypter cipher.Decrypter) (hash []byte, err error)
	ContentsHash(decrypter cipher.Decrypter) (hash []byte, err error)
	Valid() error
}
```

### Methods

#### URL

Addressable location of the message, the URL may be encrypted requiring decrypter to be supplied to decrypt URL.

**Parameters:**

| Name | Type | Notes |
| :--- | :--- | :--- |
| decrypter | [cipher.decrypter](https://godoc.org/github.com/mailchain/mailchain/crypto/cipher#Decrypter) | Used to decrypt the URL where the message can be found. Decrypter is required but is only used if the url is stored encrypted. |

**Returns:**

| **Name** | Type | Notes |
| :--- | :--- | :--- |
| url | [\*url.URL](https://godoc.org/net/url#URL) | Address of the message. _Nil if error._ |
| err | error | Error object describing the cause. |

#### In**tegrityHash**

Hash of the encrypted content. This can be used to validate the integrity of the envelope contents before decrypting. 

**Parameters:**

| Name | Type | Notes |
| :--- | :--- | :--- |
| decrypter | [cipher.decrypter](https://godoc.org/github.com/mailchain/mailchain/crypto/cipher#Decrypter) | Used to decrypt the hash, where only the intended recipient can validate the contents. Decrypter is required but is only used if the hash is stored encrypted. |

**Returns:**

| **Name** | Type | Notes |
| :--- | :--- | :--- |
| hash | [\[\]byte](https://godoc.org/builtin#byte) | Hash of the contents to validate integrity. _Nil if error._ |
| err | error | Error object describing the cause. |

{% hint style="danger" %}
Integrity Hash is not intended to be cryptographically secure, use [ContentsHash](programmable-envelopes.md#url) for a secure cryptographic hash.
{% endhint %}

#### **ContentsHash**

Hash of the decrypted content. This can be used to verify the contents of the message have not been tampered with.

**Parameters:**

| Name | Type | Notes |
| :--- | :--- | :--- |
| decrypter | [cipher.decrypter](https://godoc.org/github.com/mailchain/mailchain/crypto/cipher#Decrypter) | Used to decrypt the hash, where only the intended recipient can verify the contents. Decrypter is required but is only used if the hash is stored encrypted. |

**Returns:**

| **Name** | Type | Notes |
| :--- | :--- | :--- |
| hash | [\[\]byte](https://godoc.org/builtin#byte) | Hash of the contents to validate the message contents. _Nil if error._ |
| err | error | Error object describing the cause. |

### 



