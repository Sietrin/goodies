#### Self-Signed Certificate

Step 1: **Generate a Private Key for the Root Certificate Authority (CA):** We'll begin by generating a private key for the root CA. The root CA will be used to sign the SSL certificate for our web server.

```bash
openssl genpkey -algorithm RSA -out root-ca.key
```


Step 2: **Generate a Self-Signed Root Certificate:** With the private key for the root CA, we'll now generate a self-signed root certificate. This certificate will act as the root of trust for our web server certificate.

```bash
openssl req -x509 -new -key root-ca.key -days 3650 -out root-ca.crt
```

Step 3: **Generate a Private Key for the Web Server:** Next, let's generate a private key for the web server where we want to use the SSL certificate.

```bash
openssl genpkey -algorithm RSA -out webserver.key
```

Step 4: **Generate a Certificate Signing Request (CSR) for the Web Server:** With the web server private key, we'll generate a CSR that contains the information about the web server and the public key. This CSR will be used to create the SSL certificate.

```bash
openssl req -new -key webserver.key -out webserver.csr
```

During this step, you'll again be prompted to provide information about the certificate subject, including the Common Name (CN) which should match the domain name of your web server (e.g., example.com). This CN must match the CN used during the root CA self-signed certificate generation.

Step 5: **Create the Web Server SSL Certificate by Signing with the Root CA:** Now, we'll use the root CA certificate and key to sign the web server CSR and create the SSL certificate for the web server.

```bash
openssl x509 -req -in webserver.csr -CA root-ca.crt -CAkey root-ca.key -CAcreateserial -out webserver.crt -days 365
```

Step 6: **Configure the Web Server to Use the SSL Certificate:** 

Specify in this config the path to the certificate and web-server key 
```bash
/etc/httpd/conf.d/ssl.conf 
```

```php
SSLCertificateFile /etc/httpd/ssl/webserver.crt
SSLCertificateKeyFile /etc/httpd/ssl/webserver.key
```