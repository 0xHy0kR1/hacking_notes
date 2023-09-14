### What's a Digital Signature?
- Digital signatures are a way to prove the authenticity of files, to prove who created or modified them.
- The simplest form of digital signature would be encrypting the document with your private key, and then if someone wanted to verify this signature they would decrypt it with your public key and check if the files match.

### Certificates - Prove who you are!
- How does your web browser know that the server you’re talking to is the real tryhackme.com? The answer is certificates.
- The certificates have a chain of trust, starting with a root CA (certificate authority). Root CAs are automatically trusted by your device, OS, or browser from install. Certs below that are trusted because the Root CAs say they trust that organisation. Certificates below that are trusted because the organisation is trusted by the Root CA and so on.
Pending --> pending https -->  https://robertheaton.com/2014/03/27/how-does-https-actually-work/