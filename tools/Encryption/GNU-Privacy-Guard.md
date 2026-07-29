# GNU Privacy Guard

* The GNU Privacy Guard(opens in new tab), also known as GnuPG or GPG, implements the OpenPGP standard.

* We can encrypt a file using GnuPG (GPG) using the following command:

``` bash
gpg --symmetric --cipher-algo CIPHER message.txt
```
* where CIPHER is the name of the encryption algorithm. 
* You can check supported ciphers using the command 
```bash
gpg --version
```
* The encrypted file will be saved as message.txt.gpg.

* The default output is in the binary OpenPGP format; however, if you prefer to create an ASCII armoured output, which can be opened in any text editor, you should add the option --armor. For example, 
```bash
gpg --armor --symmetric --cipher-algo CIPHER message.txt.
```

* You can decrypt using the following command:
```bash
gpg --output original_message.txt --decrypt message.gpg
```