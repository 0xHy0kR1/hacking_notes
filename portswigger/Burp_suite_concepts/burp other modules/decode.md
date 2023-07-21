## Introduction
- we can _decode_ information that we capture during an attack, but we can also _encode_ data of our own, ready to be sent to the target.
- Decoder also allows us to create _hashsums_ of data, as well as providing a Smart Decode feature which attempts to decode provided data recursively until it is back to being plaintext.
![[burp_basics13.png]]

**This interface offers us a number of options.**
![[burp_basics14.png]]
1. The box on the left is where we would paste or type text to be encoded or decoded. As with most other modules of Burp Suite, we can also send data here from other sections of the framework by right-clicking and choosing _Send to Decoder._  
2. We have the option to select between treating the input as text or hexadecimal byte values at the top of the list on the right.
3. Further down the list, we have dropdown menus to _Encode_, _Decode_ or _Hash_ the input.
4. Finally, we have the "Smart Decode" feature, which attempts to decode the input automatically.

**Note** - 
As we add data into the input field, the interface will duplicate itself to contain the output of our transformation. We can then choose to operate on this using the same options:
![[burp_basics15.png]]

## Decoding/Encoding Methods:
![[burp_basics16.png]]

#### Basics of example - 1
**Plain:** 
	- Plaintext is what we have before performing any transformations

**URL**:
	- URL encoding is used to make data safe to transfer in the URL of a web request.
	- 
**Example-1** - let's encode the forward-slash character (`/`)
URL encoded forward-slash `%2F`
We can confirm this with Decoder by typing a forward slash in the input box, then selecting `Encode as` -> `URL`:
![[burp_basics17.png]]

**HTML:**
	- Encoding text as HTML Entities involves replacing special characters with an ampersand (`&`) followed by either a hexadecimal number or a reference to the character being escaped, then a semicolon (`;`).
**Example-2** - 
Choose `Decode as` -> `HTML`
![[burp_basics18.png]]

**Base64:**
	- base64 is used to encode any data in an ASCII-compatible format.
	- It was designed to take binary data (e.g. images, media, programs) and encode it in a format that would be suitable to transfer over virtually any medium.

**ASCII Hex:** 
	- This option converts data between ASCII representation and hexadecimal representation.

**Hex**, **Octal**, and **Binary:**
	- These encoding methods all apply only to numeric inputs.

**Gzip:**
	- Gzip provides a way to _compress_ data.
	- It is widely used to reduce the size of files and pages before they are sent to your browser.
![[burp_basics19.png]]

**Hex Format:**
"Hex View" by choosing "Hex" above the decoding options:
![[burp_basics20.png]]

---

**Smart Decode:**
	- This feature of Decoder attempts to automatically decode encoded text.

**Hashing theory** - 
- Hashing is a one-way process that is used to transform data into a unique signature.
- A good hashing algorithm will ensure that every piece of data entered will have a completely unique hash.
- hashes are also used to securely store passwords as (due to the one-way hashing process meaning that the hashes can never be reversed) the passwords will be (relatively) secure even if the database is leaked
- When a user creates a password, it is hashed and stored by the application. When the user tries to log in, the application will then hash the password they submit and check it against the stored hash; if the hashes match, then the password was correct.

## Hashing in Decoder:
- Decoder allows us to generate hashsums for data directly within Burp Suite.
- Specifically, we click on the "Hash" dropdown menu and select an algorithm from the list:
![[burp_basics22.png]]

![[burp_basics23.png]]
This is because the output of a hashing algorithm does not return pure ASCII/Unicode text. As such, it is common to take the resultant output of the algorithm and turn it into a hexadecimal string
