# Cryptography
## Use ssk-keygen to generate RSA key pair
```
ssh-keygen -t rsa -b 1024 //gererate id_rsa(private key) & id_rsa.pub
ssh-keygen -f id_rsa.pub -e -m pem //convert id_rsa.pub to PKCS#1 format (.pem)
```