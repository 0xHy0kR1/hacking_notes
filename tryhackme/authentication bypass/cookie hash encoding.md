![[hash_gen.png]]
- You can see from the above table that the hash output from the same input string can significantly differ depending on the hash method in use.
- The [https://crackstation.net/](https://crackstation.net/) keep databases of billions of hashes and their original strings.
- the hash is irreversible.

## Encoding
- Encoding is similar to hashing in that it creates what would seem to be a random string of text, but in fact, the encoding is reversible.
- Encoding allows us to convert binary data into human-readable text that can be easily and safely transmitted over mediums that only support plain text ASCII characters.
	- Common encoding types are base32 which converts binary data to the characters A-Z and 2-7
	- base64 which converts using the characters a-z, A-Z, 0-9,+, / and the equals sign for padding.
- Base64 decoding can be done with base64decode.org and encoding can be done with base64encode.org