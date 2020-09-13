# Using Certificates in JVM Applications

A JVM application (Java/Kotlin etc) manages certificates via Java KeyStore(JKS).
The JKS can contain: 
* Server certificates
  * use in TLS by client to check authenticity of the server
* Client certificates
  * used in mTLS by server to check authenticity of the client

## Keystore Formats
* JKS is proprietary but is a defacto standard for certificate containers in JVM world
* PKCS12 is a standard certificate container format

## Certificate Formats
https://www.ssls.com/knowledgebase/what-are-certificate-formats-and-what-is-the-difference-between-them/

## Keystore Commands

```sh
# list certificates
keytool -list -keystore ./some.jks

# list certifcates with details
keytool -list -v -keystore ./some.jks

# put certificate & private key into PKCS-12 key store
openssl pkcs12 -export -in blah.crt -inkey blah.key -name blah -out some.p12

# import PKCS-12 key store contents into JKS
keytool -importkeystore -srckeystore some.p12 -srcstoretype PKCS12 -destkeystore some.jks -deststorepass ${KEYSTORE_PASSWORD}
```

## Certificate Creation commands

```sh
# generate private key
openssl genrsa 2048 > blah.key

# generate CSR (certificate signing request)
openssl req -new -key blah.key -out blah.csr

# generate self signed certificate in CRT format
openssl x509 -req -days 3650 -in blah.csr -signkey blah.key -out blah.crt

# convert certificate to PEM format
openssl x509 -in blah.crt -out blah.pem

# print detail information of certificate
keytool -printcert -file blah.pem
```

## Squashing certificates
If server is unable to authenticate the client despite have the client certificate in its trust store, it could be because the client certificate chain has not been squashed correctly. The client cert chain can be squashed as shown below in the PEM file which can then be put into the server's trust store. (Be aware of there is a new line at the end of file):
```
-----BEGIN CERTIFICATE-----
<Root CA>
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
<Intermediate Cert>
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
<Client Cert>
-----END CERTIFICATE-----
```

## SSL/TLS Debugging
```sh
# check server certificate
openssl s_client -connect some.server.com:443
```
