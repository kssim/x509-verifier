# X509-Verifier

## Create OpenSSL Test Certificate
* Create Self-Signed RootCA Certificate
  1. <code>openssl genrsa -aes256 -out ./rootca.key 2048</code>
  2. <code>chmod 600 ./rootca.key</code>
  3. <code>openssl req -new -key ./rootca.key -out ./rootca.csr</code>
  4. <code>openssl x509 -req -days 3650 -extensions v3_ca -set_serial 1 -in ./rootca.csr -signkey ./rootca.key -out ./rootca.crt</code>

* Create Certificate
  1. <code>openssl genrsa -aes256 -out ./cert.key 2048</code>
  2. <code>openssl req -new -key ./cert.key -out cert.csr</code>
  3. <code>openssl x509 -req -days 730 -extensions v3_user -in ./cert.csr -CA ./rootca.crt -CAcreateserial -CAkey rootca.key -out ./cert.crt</code>

* Convert PEM to DER
  * <code>openssl x509 -inform der -in cert.pem -out cert.der</code>

* Convert DER to PEM
  * <code>openssl x509 -inform der -in cert.cer -out cert.pem</code>
  
* Create CRL
  1. <code>openssl ca -config openssl.cnf -gencrl -out root.crl.pem</code>
