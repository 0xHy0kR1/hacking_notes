- Regular Expressions is nothing but a pattern to match for each input line.
- A pattern is a sequence of characters.

**Following all are examples of pattern:**
```sh
^w1
w1|w2
[^ ]
foo
bar
[0-9]
```

### Three types of regex
**The grep understands three different types of regular expression syntax as follows:**
1. basic (BRE)
2. extended (ERE)
3. perl (PCRE)

### grep Regular Expressions Examples

1. Search for a word named ‘vivek’ in the [/etc/passwd](https://www.cyberciti.biz/faq/understanding-etcpasswd-file-format/ "Understanding /etc/passwd File Format") file:
```sh
grep 'vivek' /etc/passwd
```

**Sample outputs:**
```sh
vivek:x:1000:1000:Vivek Gite,,,:/home/vivek:/bin/bash
vivekgite:x:1001:1001::/home/vivekgite:/bin/sh
gitevivek:x:1002:1002::/home/gitevivek:/bin/sh
```

2. Next, search for a word named ‘vivek’ in any case (i.e. case insensitive search):
```sh
grep -i -w 'vivek' /etc/passwd
```

3. Let us try to search two words ‘vivek’ or ‘raj’ in any case:
```sh
grep -E -i -w 'vivek|raj' /etc/passwd
```

4. The following will match word Linux or UNIX in any case using the [egrep command](https://www.cyberciti.biz/faq/grep-regular-expressions/ "Regular expressions in grep ( regex ) with examples"):
```sh
egrep -i '^(linux|unix)' filename  
# Same as above by passing the '-E' to the grep #  
grep -E -i '^(linux|unix)' filename
```

### A note about egrep vs. grep -E syntax
**The latest version of egrep will show the following warning**
```sh
egrep: warning: egrep is obsolescent; using grep -E
Usage: grep [OPTION]... PATTERNS [FILE]...
Try 'grep --help' for more information.
```

**You need to update all your scripts and command to use the following syntax. From:**
```sh
egrep -i 'foo|bar' /path/to/file
```

**To (avoid using the egrep):**
```sh
grep -E -i 'foo|bar' /path/to/file
```

### How to match single characters
**The . character (period, or dot) matches any one character. Consider the following demo.txt file:**
```sh
cat demo.txt
```

**Sample outputs:**
```sh
foo.txt
bar.txt
foo1.txt
bar1.doc
foobar.txt
foo.doc
bar.doc
dataset.txt
purchase.db
purchase1.db
purchase2.db
purchase3.db
purchase.idx
foo2.txt
bar.txt
```

**Let us find all filenames starting with purchase, type:**
```sh
grep 'purchase' demo.txt
```

**Next I need to find all filenames starting with purchase and followed by another character:**
```sh
grep 'purchase.db' demo.txt
```

**Our final example find all filenames starting with purchase but ending with db:**
```sh
grep 'purchase..db' demo.txt
```

![[regex1.webp]]
### How to match only dot (.)
- A dot (.) has a special meaning in regex, i.e. match any character.
- But, what if you need to match dot (.) only? I want to tell my grep command that I want actual dot (.) character and not the regex special meaning of the . (dot) character.
- You can escape the dot (.) by preceding it with a \ (backslash):
```sh
grep 'purchase..' demo.txt  
grep 'purchase.\.' demo.txt
```

![[regex2.webp]]

## Anchors

1. You can use ^ and $ to force a regex to match only at the start or end of a line, respectively. The following example displays lines starting with the vivek only:
```sh
grep ^vivek /etc/passwd
```

**Sample outputs:**
```sh
vivek:x:1000:1000:Vivek Gite,,,:/home/vivek:/bin/bash
vivekgite:x:1001:1001::/home/vivekgite:/bin/sh
```

2. You can display only lines starting with the word vivek only i.e. do not display vivekgite, vivekg etc:
```sh
grep -w ^vivek /etc/passwd
```

3. Find lines ending with word foo:
```sh
grep 'foo$' filename
```

4. Match line only containing foo:
```sh
grep '^foo$' filename
```

5. You can search for blank lines with the following examples:
```sh
grep '^$' filename
```

## How to match sets of character using grep
- You can match specific characters and character ranges using [..] syntax.

1. Say you want to Match both ‘Vivek’ or ‘vivek’:
```sh
grep '[vV]ivek' filename
```
OR
```sh
grep '[vV][iI][Vv][Ee][kK]' filename
```

**Let us match digits and upper and lower case characters.**

1. For example, try to math words such as vivek1, Vivek2 and so on:
```sh
grep -w '[vV]ivek[0-9]' filename
```

2. In this example match two numeric digits. In other words match foo11, foo12, foo22 and so on, enter:
```sh
grep 'foo[0-9][0-9]' filename
```

3. You are not limited to digits, you can match at least one letter:
```sh
grep '[A-Za-z]' filename
```

4. Display all the lines containing either a “w” or “n” character:
```sh
grep [wn] filename
```


Within a bracket expression, the name of a character class enclosed in “[:” and “:]” stands for the list of all characters belonging to that class

**Standard character class names are:**
- **[[:alnum:]]** – Alphanumeric characters.
- **[[:alpha:]]** – Alphabetic characters
- **[[:blank:]]** – Blank characters: space and tab.
- **[[:digit:]]** – Digits: ‘0 1 2 3 4 5 6 7 8 9’.
- **[[:lower:]]** – Lower-case letters: ‘a b c d e f g h i j k l m n o p q r s t u v w x y z’.
- **[[:space:]]** – Space characters: tab, newline, vertical tab, form feed, carriage return, and space.
- **[[:upper:]]** – Upper-case letters: ‘A B C D E F G H I J K L M N O P Q R S T U V W X Y Z’.

1. In this example match all upper case letters:
```sh
grep '[:upper:]' filename
```

### How negates matching in sets
1. The ^ negates all ranges in a set:
```sh
grep '[vV]ivek[^0-9]' test
```

![[regex3.webp]]

## Wildcards
1. You can use the “.” for a single character match. In this example match all 3 character word starting with “b” and ending in “t”: