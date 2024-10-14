# Security

## OAuth 2.0

- <https://blog.postman.com/what-is-oauth-2-0/>

## Access token

- An artifact that client applications can use to make secure calls to an API server.
- When a client application needs to access protected resources on a server on behalf of a user, the access token lets the client signal to the server that it has received authorization by the user to perform certain tasks or access certain resources.

## Refresh token

- <https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/>

- Access tokens may be valid for a short amount of time.
- Once they expire, client applications can use a refresh token to "refresh" the access token.
- Refresh Token Rotation
- Refresh Token Automatic Reuse Detection

## Authorization control flow with PKCE (for Apps)

- <https://blog.postman.com/what-is-pkce/>

- Client creates and stores a secret called the “code verifier.”
  - Code verifier is a cryptographically random string that the client uses to identify itself when exchanging an authorization code for an access token.
  - It has a minimum length of 43 characters and a maximum length of 128 characters.
- Client also generates a code challenge, which is a transformation of the code verifier.
- Code challenge is sent with the initial authorization request, along with a code challenge method.
  - Code challenge method is the transformation mode used to generate the code challenge. There are two code challenge methods that PKCE supports: plain and S256.
  - Prefer S256.
  - S256: SHA-256 hash of the code verifier is encoded using the BASE64URL encoding.
- Code challenge is securely stored by the authorization server, and an authorization code is returned with the redirect URL as usual.
- When the client wants to exchange this authorization code for the access token, it sends a request that includes the initial code verifier.
- The server then hashes the code verifier using SHA-256 and encodes the hashed value as a BASE64URL.
- The corresponding value is then compared to the code challenge. If they match, an access token is issued. Otherwise, an error message is returned.
- This flow ensures that a malicious third-party application cannot exchange an authorization code for an access token, since the malicious application does not have the code verifier.
- Intercepting the code challenge is also useless because SHA256 is a one-way hashing algorithm and cannot be decrypted.

## CSRF (Cross-site request forgery)

## Hashing Passwords

When hashing passwords, salts are used to add an extra layer of security. Here’s a basic process on how to use salts when hashing:

1. Generate a Salt: Use a Cryptographically Secure Pseudo-Random Number Generator (CSPRNG) to produce a salt2. The salt should be unique for each user password.
2. Combine Salt and Password: Add the salt to the beginning or the end of the password3.
3. Hash the Combination: Hash the combination of the salt and the password using a secure hash function, such as Scrypt, Argon2 or SHA-2562.
4. Store the Salt and Hash: Save both the salt and the hash in your user database2. When the user logs in again, you will need to retrieve the salt, append it to the provided password, hash the result, and compare it to the stored hash

## Encryption

- <https://cloud.google.com/docs/security/encryption/default-encryption?hl=en>
- <https://cloud.google.com/docs/security/encryption-in-transit?hl=en>

### Encryption at rest

Protects your data from a system compromise or data exfiltration by encrypting data while stored. The Advanced Encryption Standard (AES) is often used to encrypt data at rest.

### Encryption in transit

Protects your data if communications are intercepted while data moves between your site and the cloud provider or between two services. This protection is achieved by encrypting the data before transmission; authenticating the endpoints; and, on arrival, decrypting and verifying that the data was not modified. For example, Transport Layer Security (TLS) is often used to encrypt data in transit for transport security, and Secure/Multipurpose Internet Mail Extensions (S/MIME) is used often for email message encryption.

### Encryption in use

Protects your data in memory from compromise or data exfiltration by encrypting data while being processed. For more information, see Confidential Computing.

## OWASP Secure Coding Principles

- Input Validation
- Output Encoding
- Authentication and Password Management
- Session Management
- Access Control
- Cryptographic Practices
- Error Handling and Logging
- Data Protection
- Communication Security
- System Configuration
- Database Security
- File Management
- Memory Management
- General Coding Practices

## HTTP Host Header attack (Host Header Injection)

- An HTTP Host Header attack occurs when an attacker manipulates the value of the Host header in an HTTP request to gain unauthorized access or influence server behavior
- The Host header is a mandatory request header in HTTP/1.1 that specifies the domain name the client wants to access
- If a web application doesn't properly validate or sanitize the Host header, an attacker can inject malicious payloads that manipulate server-side behavior

## HSTS (Strict-Transport-Security header)

- The primary purpose of the HSTS header is to instruct browsers to interact with a website only over HTTPS, preventing any communication over insecure HTTP connections

## Clickjacking

- Clickjacking, also known as UI redress attack, is a malicious technique that tricks users into clicking on invisible buttons or links on a webpage

## Cross-Site Scripting

## SQL Injection

## HTTP Response Splitting

## Content Spoofing

## Information Leaking

## SSL

### Generate Self-signed SSL Certificate

- Generate a Private Key and a CSR (Certificate Signing Request): Use the following command to generate a new private key mykey.pem and a CSR mycsr.csr:

```bash
openssl req -new -newkey rsa:2048 -nodes -keyout mykey.pem -out mycsr.csr -subj "/C=BR/ST=Sao Paulo/L=Sao Paulo/O=PTW/CN=localhost"
```

In this example, C is for Country, ST is for State, L is for Locality or city, O is for Organization, and CN is for Common Name which is usually the domain name.

- Generate a Self-Signed Certificate: Now, use the following command to generate a self-signed certificate mycert.pem that is valid for 365 days:

```bash
openssl x509 -req -days 365 -in mycsr.csr -signkey mykey.pem -out mycert.pem
```

Now, mycert.pem is your self-signed certificate and mykey.pem is your private key.

- Combine the Private Key and the Certificate into a Single PEM File:

```bash
cat mycert.pem mykey.pem > mongo.pem
```
