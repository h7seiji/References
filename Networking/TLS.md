# Transport Layer Security (TLS)

SSL (Secure Socket Layer) and its successor TLS (Transport Layer Security) are two cryptographic protocols.
Both rely on a set of private and public keys to turn messages into useless strings of characters.

The TLS protocol is designed to provide three essential services to all applications running above it:

- Encryption
- Authentication
- Integrity

## TLS Handshake

Uses public key cryptography (also known as asymmetric key cryptography), which allows the peers to negotiate a shared secret key without having to establish any prior knowledge of each other, and to do so over an unencrypted channel.
