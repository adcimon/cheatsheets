# Cryptography

[Cryptography](https://en.wikipedia.org/wiki/Cryptography) is the practice and study of techniques for secure communication protocols that prevent third parties or the public from reading private messages.

## Transport Layer Security (TLS)

[Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security) is a cryptographic protocol designed to provide communications security over a computer network. It is used as the security layer in [HTTPS](https://en.wikipedia.org/wiki/HTTPS) and [WSS](https://en.wikipedia.org/wiki/WebSocket).

## OpenSSL

[OpenSSL](https://www.openssl.org/) is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library.

Create a Certificate Signing Request (CSR).
```
openssl req -new -nodes -newkey rsa:2048 -keyout private.key -out request.csr
```
* `req` specifies the use of X.509 certificate signing request (CSR) management. The X.509 is a public key infrastructure standard that SSL and TLS adheres to for its key and certificate management.
* `-new` specifies the generation of a certificate signing request (CSR).
* `-nodes` skips the option to secure our certificate with a passphrase requesting user intervention.
* `-newkey rsa:2048` generates a new certificate and a new key at the same time (required to sign the certificate), `rsa:2048` makes an RSA key that is 2048 bits long.
* `-keyout` specifies the name of the generated private key file.
* `-out` specifies the name of the generated request file.

Create a self-signed certificate.
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate.crt
```
* `req` specifies the use of X.509 certificate signing request (CSR) management. The X.509 is a public key infrastructure standard that SSL and TLS adheres to for its key and certificate management.
* `-x509` specifies the generation of a self-signed certificate instead of generating a certificate signing request (CSR), as would normally happen.
* `-nodes` skips the option to secure our certificate with a passphrase requesting user intervention.
* `-days` sets the length of time that the certificate will be considered valid.
* `-newkey rsa:2048` generates a new certificate and a new key at the same time (required to sign the certificate), `rsa:2048` makes an RSA key that is 2048 bits long.
* `-keyout` specifies the name of the generated private key file.
* `-out` specifies the name of the generated certificate file.
