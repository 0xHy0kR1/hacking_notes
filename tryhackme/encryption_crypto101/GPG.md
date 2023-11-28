## Introduction
- GnuPG or GPG an Open Source implementation of PGP from the GNU project.
- With PGP/GPG, private keys can be protected with passphrases in a similar way to SSH private keys.
- If the key is passphrase protected, you can attempt to crack this passphrase using John The Ripper and gpg2john.

## Reading the protected file with gpg
**First we need to import the key by using the following command:**
```python
gpg --import tryhackme.key
```

**We can then read the message by using the gpg terminal command:**
```python
gpg --output message.txt --decrypt message.gpg
```

### Example
Let's suppose, we are inside a machine which require horizontal privilege escalation and we need to escalate our privilege from "skyfuck" to "merlin".

For further practical demonstration see file "/home/hoax/writeups/thm/easy/tomghost/user_own_by_ghostcat(CVE-2020-1938)" file.