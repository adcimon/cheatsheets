# Security

[Computer security](https://en.wikipedia.org/wiki/Computer_security) (also known as cybersecurity) is the protection of computer software, systems and networks from threats that can lead to unauthorized information disclosure, theft or damage to hardware, software, or data, as well as from the disruption or misdirection of the services they provide.

## Index

* [API Keys](#api_keys)
* [JWT](#jwt)
* [TLS](#tls)
  * [OpenSSL](#openssl)
* [References](#references)

## API Keys

[API keys](https://en.wikipedia.org/wiki/API_key) are secret unique identifiers used to authenticate and authorize a user, developer, or calling program to an API.

## JWT

[JSON Web Tokens (JWT)](https://en.wikipedia.org/wiki/JSON_Web_Token) are an open, industry standard method for representing claims securely between two parties. [JWT.IO](https://jwt.io/) allows to decode, verify and generate tokens.

## TLS

[Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security) is a cryptographic protocol designed to provide communications security over a computer network. It is used as the security layer in [HTTPS](https://en.wikipedia.org/wiki/HTTPS) and [WSS](https://en.wikipedia.org/wiki/WebSocket).

### OpenSSL

[OpenSSL](https://www.openssl.org/) is a robust, commercial-grade, and full-featured toolkit for the [Transport Layer Security (TLS)](https://en.wikipedia.org/wiki/Transport_Layer_Security) and [Secure Sockets Layer (SSL)](https://en.wikipedia.org/wiki/Transport_Layer_Security) protocols. It is also a general-purpose cryptography library.

Create a [Certificate Signing Request (CSR)](https://en.wikipedia.org/wiki/Certificate_signing_request).
```
openssl req -new -nodes -newkey rsa:2048 -keyout private.key -out request.csr
```
* `req` specifies the use of X.509 certificate signing request management. The X.509 is a public key infrastructure standard that SSL and TLS adheres to for its key and certificate management.
* `-new` specifies the generation of a certificate signing request.
* `-nodes` skips the option to secure our certificate with a passphrase requesting user intervention.
* `-newkey rsa:2048` generates a new certificate and a new key at the same time (required to sign the certificate), `rsa:2048` makes an RSA key that is 2048 bits long.
* `-keyout` specifies the name of the generated private key file.
* `-out` specifies the name of the generated request file.

Create a self-signed certificate.
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate.crt
```
* `req` specifies the use of X.509 certificate signing request management. The X.509 is a public key infrastructure standard that SSL and TLS adheres to for its key and certificate management.
* `-x509` specifies the generation of a self-signed certificate instead of generating a certificate signing request, as would normally happen.
* `-nodes` skips the option to secure our certificate with a passphrase requesting user intervention.
* `-days` sets the length of time that the certificate will be considered valid.
* `-newkey rsa:2048` generates a new certificate and a new key at the same time (required to sign the certificate), `rsa:2048` makes an RSA key that is 2048 bits long.
* `-keyout` specifies the name of the generated private key file.
* `-out` specifies the name of the generated certificate file.

<p align="center"><img align="center" width="90%" height="90%" src="assets/certificate_diagram.png"></p>

## References

* [The Copenhagen Book](https://thecopenhagenbook.com)
