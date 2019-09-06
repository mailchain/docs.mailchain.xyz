# Types

## Message Location Identifier

Data stored in a transaction costs. Encoding [https://message-location-domain.com/](https://message-location-domain.com/) is inefficient due to each char needs 1 byte for storage. A reasonable minimum domain name with a length of 3, minimum top level domain \(TLD\) size 2, plus schema 4/5 \(e.g. http/https\), and separators "://". The minimum expected size is 15, e.g. [https://mcx.mx/](https://mcx.mx/). A unsigned int of variable size can represent 18446744073709551615 mappings in a max of 10 bytes.  


## Uint64Bytes

Typed tuple that combines a variable sized integer and byte array in a single byte array to reduce the number of bytes needed to store both fields. The motivation behind this data type is to reduce the padding requirements to encrypt a variable sized integer.



