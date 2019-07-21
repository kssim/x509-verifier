# X509-Verifier

## Create OpenSSL Test Certificate
* Create Self-Signed RootCA Certificate
  1. openssl genrsa -aes256 -out ./rootca.key 2048
  2. chmod 600 ./rootca.key
  3. openssl req -new -key ./rootca.key -out ./rootca.csr
  4. openssl x509 -req -days 3650 -extensions v3_ca -set_serial 1 -in ./rootca.csr -signkey ./rootca.key -out ./rootca.crt

* Create Certificate
  1. openssl genrsa -aes256 -out ./cert.key 2048
  2. openssl req -new -key ./cert.key -out cert.csr
  3. openssl x509 -req -days 730 -extensions v3_user -in ./cert.csr -CA ./rootca.crt -CAcreateserial -CAkey rootca.key -out ./cert.crt

* Convert PEM to DER
  * openssl x509 -inform der -in cert.pem -out cert.der

* Convert DER to PEM
  * openssl x509 -inform der -in cert.cer -out cert.pem
