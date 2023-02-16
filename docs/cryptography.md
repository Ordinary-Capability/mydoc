# Cryptography
## Generate RSA key pair
- Use ssh-keygen to generate key pair
```
ssh-keygen -t rsa -b 1024 //gererate id_rsa(private key), id_rsa.pub
```
- Use openssl to extract PKCS@1 pub key as .pem file
```
openssl rsa -in id_rsa -pubout -out id_rsa.pub.pem
```
