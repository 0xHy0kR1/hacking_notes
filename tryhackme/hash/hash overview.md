## What's a hash function?
- Hash functions are quite different from encryption. There is no key, and it’s meant to be impossible (or very very difficult) to go from the output back to the input.
- A hash function takes some input data of any size, and creates a summary or "digest" of that data. The output is a fixed size.
- Good hashing algorithms will be (relatively) fast to compute, and slow to reverse (Go from output and determine input).
- The output of a hash function is normally raw bytes, which are then encoded. Common encodings for this are base 64 or hexadecimal. Decoding these won’t give you anything useful.

## What's a hash collision?
- A hash collision is when 2 different inputs give the same output. Hash functions are designed to avoid this as best as they can.
- Due to the pigeonhole effect, collisions are not avoidable.

## Basic terms
**Ciphertext** - The result of encrypting a plaintext, encrypted data

**Cipher** - A method of encrypting or decrypting data. Modern ciphers are cryptographic, but there are many non cryptographic ciphers like Caesar.

**Plaintext** - Data before encryption, often text but not always. Could be a photograph or other file

**Encryption** - Transforming data into ciphertext, using a cipher.

**Encoding** - NOT a form of encryption, just a form of data representation like base64. Immediately reversible.

**Key** - Some information that is needed to correctly decrypt the ciphertext and obtain the plaintext.

**Passphrase** - Separate to the key, a passphrase is similar to a password and used to protect a key.

**Asymmetric encryption** - Uses different keys to encrypt and decrypt.

**Symmetric encryption** - Uses the same key to encrypt and decrypt

**Brute force** - Attacking cryptography by trying every different password or every different key

**Cryptanalysis** - Attacking cryptography by finding a weakness in the underlying maths