# Cryptography

[Cryptography](https://en.wikipedia.org/wiki/Cryptography) is the practice and study of techniques for secure communication protocols that prevent third parties or the public from reading private messages.

## Transport Layer Security (TLS)

[Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security) is a cryptographic protocol designed to provide communications security over a computer network. It is used as the security layer in [HTTPS](https://en.wikipedia.org/wiki/HTTPS) and [WSS](https://en.wikipedia.org/wiki/WebSocket).

## OpenSSL

[OpenSSL](https://www.openssl.org/) is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library.

Create a self certificate.
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate.crt
```
* `req` This subcommand specifies that we want to use X.509 certificate signing request (CSR) management. The “X.509” is a public key infrastructure standard that SSL and TLS adheres to for its key and certificate management. We want to create a new X.509 cert, so we are using this subcommand.
* `x509` This further modifies the previous subcommand by telling the utility that we want to make a self-signed certificate instead of generating a certificate signing request, as would normally happen.
* `nodes` This tells OpenSSL to skip the option to secure our certificate with a passphrase. We need Apache to be able to read the file, without user intervention, when the server starts up. A passphrase would prevent this from happening because we would have to enter it after every restart.
* `days` This option sets the length of time that the certificate will be considered valid.
* `newkey rsa:2048` This specifies that we want to generate a new certificate and a new key at the same time. We did not create the key that is required to sign the certificate in a previous step, so we need to create it along with the certificate. The rsa:2048 portion tells it to make an RSA key that is 2048 bits long.
* `keyout` This line tells OpenSSL where to place the generated private key file that we are creating.
* `out` This tells OpenSSL where to place the certificate that we are creating.
