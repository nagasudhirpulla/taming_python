# Create a self-signed SSL certificate with OpenSSL
- In this post we will explore how to create a self-signed SSL certificate files using OpenSSL

- OpenSSL is a toolkit for cryptography

## What is a self-signed certificate

- A self-signed certificate is a digital certificate that is signed by its own creator, rather than a trusted third-party Certificate Authority (CA). They are often used in development and testing environments where CA is not necessary

- The following files will be generated for a self-signed certificate

	- `cert.pem` - Certificate file. This contains the public key, certificate information like subject, department, Organizational unit, country etc.

	- `key.pem` - encrypted private key file. This contains the private key

	- `certificate.pfx` - contains both certificate and private key information in a single file

## Install OpenSSL

- OpenSSL can be downloaded for windows at https://slproweb.com/products/Win32OpenSSL.html

- OpenSSL also comes in-built with git bash

- OpenSSL can be installed in debian  linux operating systems using the following commands

```bash

sudo apt update

sudo apt install openssl  libssl-dev

```

## Certificate and private key files generation

### Command for Interactive mode

- Upon running the following command, the files cert.pem and key.pem are generated after answering the questions by openssl.

```bash

openssl req -x509 -newkey rsa:4096 -keyout  key.pem -out cert.pem -sha256 -days 365

```

### Command for Non-interactive and 10 years expiration

```bash

openssl req -x509 -newkey rsa:4096 -keyout  key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"

```

## Create pfx file from certificate and key files

- The following command creates the pfx file (certificate.pfx) from key.pem and cert.pem files

```bash

openssl pkcs12 -export -out certificate.pfx -inkey  key.pem -in cert.pem

```

### Check PFX contents:

- Run the following command to check if the pfx file is valid and the contents of pfx file

```bash

openssl pkcs12 -info -in certificate.pfx

```

## References

- OpenSSL download for windows - https://slproweb.com/products/Win32OpenSSL.html

- OpenSSL docs - https://docs.openssl.org/master/man1/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNTgzNzQ4MzUsLTYzMDA2NTg5NiwtMT
U4MTM4OTgyNF19
-->