## Vulnerable Functions
**In PHP, many functions interact with the operating system to execute commands via shell; these include:**
- Exec
- Passthru
- System

**Example** - 
Here, the application will only accept and process numbers that are inputted into the form. This means that any commands such as `whoami` will not be processed.
![[ci5.png]]
1. The application will only accept a specific pattern of characters (the digits  0-9)
2. The application will then only proceed to execute this data which is all numerical.

**Note** - Any application that uses these functions without proper checks will be vulnerable to command injection.

## Input sanitisation
This is a process of specifying the formats or types of data that a user can submit. 

**Example** -  
an input field that only accepts numerical data or removes any special characters such as `>` ,  `&` and `/`.
`filter_input` [PHP function](https://www.php.net/manual/en/function.filter-input.php) is used to check whether or not any data submitted via an input form is a number or not. If it is not a number, it must be invalid input.
![[ci6.png]]

## Bypassing Filters
- These filters will restrict you to specific payloads; however, we can abuse the logic behind an application to bypass these filters.

**Example** - 
an application may strip out quotation marks; we can instead use the hexadecimal value of this to achieve the same result.
![[ci7.png]]

