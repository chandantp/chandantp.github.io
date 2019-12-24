
# Openssl Useful Commands

```bash
# openssl version
OpenSSL 1.0.2k-fips  26 Jan 2017
```

#### Certificate Signing Request(CSR) & Private Key
Create below configuration file `test.conf`:
```json
[ req ]
distinguished_name      = req_distinguished_name
prompt                  = no
req_extensions          = v3_req
 
[ req_distinguished_name ]
countryName             = AU
stateOrProvinceName     = Victoria
localityName            = Melbourne
0.organizationName      = chandantp
organizationalUnitName  = My Organisation
commonName              = hello.chandantp.com.au
emailAddress            = chandan.tp@gmail.com
 
[ v3_req ]
# Extensions to add to a certificate request
basicConstraints        = CA:FALSE
keyUsage                = nonRepudiation, digitalSignature
```

Run below command for creating the private key(`test.key`) and corresponding CSR(`test.csr`):
```bash
# openssl req -newkey rsa:2048 -sha256 -nodes -config test.conf -keyout test.key -out test.csr
```

Use the CSR as input to create a certificate:
```
TODO
```

Use below commands to verify if a private key matches a certificate (PEM) and CSR:
```bash
# openssl rsa -noout -modulus -in test.key | openssl md5
9349c4ad6d41cfe36ad6dad6d4122a88
 
# openssl x509 -noout -modulus -in test.pem | openssl md5
9349c4ad6d41cfe36ad6dad6d4122a88
 
# openssl req -noout -modulus -in test.csr | openssl md5
9349c4ad6d41cfe36ad6dad6d4122a88
```