## Introduction
- In John the Ripper, custom rules are special techniques used to generate variations of words from a wordlist.
- These variations help the password-cracking process by trying different combinations of characters, making it more effective in finding weak passwords.

## How to create Custom Rules
Custom rules are defined in the `john.conf` file, usually located in `/etc/john/john.conf`

**The first line:**
`[List.Rules:THMRules]` - Is used to define the name of your rule, this is what you will use to call your custom rule as a John argument.

We then use a regex style pattern match to define where in the word will be modified, again- we will only cover the basic and most common modifiers here:

1. **Az Rule:**
	- The Az rule appends characters to the end of each word in the wordlist.
	- For example, if the wordlist contains "apple" and you apply the Az rule with "123," it will generate variations like "apple123," "apple1," "apple2," and so on.
2. **A0 Rule:**
	- The A0 rule prepends characters to the beginning of each word in the wordlist.
	- For example, if the wordlist contains "pass" and you apply the A0 rule with "99," it will generate variations like "99pass," "991pass," "992pass," and so on.
3. **c Rule:**
	- The c rule capitalizes different characters positionally in the word.
	- For example, if the wordlist contains "hello," applying the c rule will generate variations like "Hello," "hEllo," "heLlo," "helLo," and "hellO."

**Defining Characters to Append, Prepend, or Include**
- After specifying a modifier like `Az` (append) or `A0` (prepend), you need to define what characters should be appended, prepended, or included in the word.
- You do this by adding character sets inside square brackets `[ ]` in the order they should be used.
	**Examples of character sets**
	- `[0-9]`: This includes any number from 0 to 9.
	- `[0]`: This includes only the number 0.
	- `[A-z]`: This includes both uppercase and lowercase letters.
	- `[A-Z]`: This includes only uppercase letters.
	- `[a-z]`: This includes only lowercase letters.
	- `[a]`: This includes only the letter "a".
	- `[!£$%@]`: This includes the symbols `!`, `£`, `$`, `%`, and `@`.

#### Example
Let's consider the custom rule `[List.Rules:PoloPassword]` again: `cAz"[0-9] [!£$%@]"`.
**Above regex explaination** - 
- It first capitalizes the first letter using `c`.
- Then, it appends a number from 0 to 9 using `Az` and the `[0-9]` character set.
- Finally, it appends a symbol from the set `[!£$%@]` using `Az` and the `[!£$%@]` character set.