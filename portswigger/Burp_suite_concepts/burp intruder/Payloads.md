## Payload sets
1. **Payload Sets**:
	- This section allows us to choose which position we want to configure a set for as well as what type of payload we would like to use.
	- For Sniper or Battering Ram --> the dropdown menu for "Payload Set" will only have one option.
**Example** -
with two positions (_`username=§pentester§&password=§Expl01ted§`_), the first item in the payload set dropdown would refer to the username field, and the second would refer to the password field.

2. **Payload type**:
	- The second dropdown in this section allows us to select a "payload type".
	- By default, this is a "Simple list" -- which, as the name suggests, lets us load in a wordlist to use.
![[burp_basics8.png]]

## Payload settings    
- Payload settings differ depending on the payload type we select.
![[burp_basics9.png]]
- We can payloads manually using the "Add" text box, paste lines in with "Paste", or "Load..." from a file.
- The "Remove" button removes the currently selected line only.
- The "Clear" button clears the entire list.

## Payload processing
![[burp_basics10.png]]
- It allows us to define rules to be applied to each payload in the set before being sent to the target.
- **Example** - we could capitalise every word or skip the payload if it matches a regex.

## Payload Encoding
- This section allows us to override the default URL encoding options that are applied automatically to allow for the safe transmission of our payload.
- Sometimes it can be beneficial to _not_ URL encode these standard "unsafe" characters.
![[burp_basics11.png]]
