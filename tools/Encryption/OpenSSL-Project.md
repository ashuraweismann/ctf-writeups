# OpenSSL Project

* The OpenSSL Project(opens in new tab) maintains the OpenSSL software.

* We can encrypt a file using OpenSSL using the following command:
```bash
openssl aes-256-cbc -e -in message.txt -out encrypted_message
```
* We can decrypt the resulting file using the following command:
```bash
openssl aes-256-cbc -d -in encrypted_message -out original_message.txt
```
* To make the encryption more secure and resilient against brute-force attacks, we can add ```bash-pbkdf2``` to use the Password-Based Key Derivation Function 2 (PBKDF2); moreover, we can specify the number of iterations on the password to derive the encryption key using ```bash-iter NUMBER```. To iterate 10,000 times, the previous command would become:
```bash
openssl aes-256-cbc -pbkdf2 -iter 10000 -e -in message.txt -out encrypted_message
```
* Consequently, the decryption command becomes:
```bash
openssl aes-256-cbc -pbkdf2 -iter 10000 -d -in encrypted_message -out original_message.txt
```