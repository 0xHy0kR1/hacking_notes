### The three main formats are:
  1. Normal
  2. Grepable (`grep`able)
  3. XML
  
There is a fourth one that we cannot recommend:

- Script Kiddie

#### 1. Normal
   - You can save your scan in normal format by using `-oN FILENAME`. N stands for normal.
   ![[nmap46.png]]

#### 2. Grepable
   - The grepable format has its name from the command `grep`; grep stands for Global Regular Expression Printer.
   - In simple terms, it makes filtering efficient.
   - You can save the scan result in grepable format using `-oG FILENAME`.
   - The normal output is 21 lines; however, the grepable output is only 4 lines. The main reason is that Nmap wants to make each line meaningful and complete when the user applies `grep`. As a result, in grepable output, the lines are so long and are not convenient to read compared to normal output.
     ![[nmap47.png]]

   - An example use of `grep` is `grep KEYWORD TEXT_FILE`;
```python
pentester@TryHackMe$ grep http 10.10.6.137_scan.nmap  80/tcp  open  http    nginx 1.6.2 OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
```

#### 3. XML
   - You can save the scan results in XML format using `-oX FILENAME`.
   - Conveniently enough, you can save the scan output in all three formats using `-oA FILENAME` to combine `-oN`, `-oG`, and `-oX` for normal, grepable, and XML.

#### 4. Script Kiddie
  You can use it to save the output of the scan `nmap -sS 127.0.0.1 -oS FILENAME`, display the output filename, and look 31337 in front of friends who are not tech-savvy.
  ![[nmap48.png]]

