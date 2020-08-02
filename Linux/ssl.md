# SSL

## openssl

Get cert from keystore

    openssl pkcs12 -in filename.jks -nokeys -out filename_cert.pem

Get key from keystore

    openssl pkcs12 -in filename.jks -nodes -nocerts -out filename_key.pem

PEM to DER

    openssl x509 -in cert.crt -outform der -out cert.der

DER to PEM

    openssl x509 -in cert.crt -inform der -outform pem -out cert.pem

View DER

    openssl x509 -in certificate.der -inform der -text -noout

Encrypt private key

    openssl pkey -aes256 -in servenc.key -out serv.key

Decrypt private key

    openssl pkey -in servenc.key -out serv.key
