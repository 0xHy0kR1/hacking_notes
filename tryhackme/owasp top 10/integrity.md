## JWT token
- JWTs are very simple tokens that allow you to store key-value pairs on a token that provides integrity as part of the token.
- The structure of a JWT token is formed of 3 parts:
![[owasp5.png]]
- The header contains metadata indicating this is a JWT, and the signing algorithm in use is HS256.
- If you change the payload, the web application can verify that the signature won't match the payload and know that you tampered with the JWT.
- Notice that each of the 3 parts of the token is simply plaintext encoded with base64.

## JWT and the None Algorithm
- A data integrity failure vulnerability was present on some libraries implementing JWTs a while ago.
- As we have seen, JWT implements a signature to validate the integrity of the payload data.
	- The vulnerable libraries allowed attackers to bypass the signature validation by changing the two following things in a JWT:
		1. Modify the header section of the token so that the `alg` header would contain the value `none`.
		2. Remove the signature part.
**Example** - 
Taking the JWT from before as an example, if we wanted to change the payload so that the username becomes "admin" and no signature check is done.
we would have to decode the header and payload, modify them as needed, and encode them back. 
Notice how we removed the signature part but kept the dot at the end.
![[owasp6.png]]

`eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0IiwiZXhwIjoxNjY1MDc2ODM2fQ.C8Z3gJ7wPgVLvEUonaieJWBJBYt5xOph2CpIhlxqdUw`