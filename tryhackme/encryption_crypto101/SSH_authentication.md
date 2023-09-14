### Encryption and SSH authentication
- This uses public and private keys to prove that the client is a valid and authorised user on the server
- By default, SSH keys are RSA keys. You can choose which algorithm to generate, and/or add a passphrase to encrypt the SSH key.
**Note** - `ssh-keygen` is the program used to generate pairs of keys most of the time.

### SSH Private Keys
- You should treat your private SSH keys like passwords. Don’t share them.
- It’s very important to mention that the passphrase to decrypt the key isn’t used to identify you to the server at all, all it does is decrypt the SSH key. The passphrase is never transmitted, and never leaves your system.

### How do I use these keys?
- The ~/.ssh folder is the default place to store these keys for OpenSSH.
- The `authorized_keys` file in this directory holds public keys that are allowed to access the server if key authentication is enabled
**Note** - Normally for the root user, only key authentication is enabled.

- In order to use a private SSH key, the permissions must be set up correctly otherwise your SSH client will ignore the file with a warning (600 or stricter).
- `ssh -i keyNameGoesHere user@host` is how you specify a key for the standard Linux OpenSSH client.

## Practical on key creation and login with SSH key
Create the keys by running:
```python
ssh-keygen
```
![[ssh-key-gen.webp]]
This create a public and private key on your machine at the following directory: **_~/.ssh_**

**We need to copy the public key to the server:**
```python
scp ~/.ssh/id_rsa.pub tryhackme@10.10.125.203:~/.ssh/authorized_keys
```

**Enter the password if you get a prompt.**
![[ssh-key-gen2.webp]]

**Now we should be able to log in with the keys, instead of the password.**
```python
ssh tryhackme@10.10.125.203
```

**If you have problems, there might be a problem with the permissions. In this case run something similar to this:**
```python
chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys
```
![[ssh-key-gen3.webp]]
