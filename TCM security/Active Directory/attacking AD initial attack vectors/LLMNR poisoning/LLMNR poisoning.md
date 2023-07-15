## Steps to perform LLMNR poisoning practically:
![[AD_in2.png]]
![[AD_in_LLMNR1.png]]
![[AD_in_LLMNR2.png]]
![[AD_in_LLMNR3.png]]

## Below performing on lab:
1. Starting the responder:
![[AD_in_LLMNR_prac2.png]]

2. Client tries to connect to attacker SMB server:
![[AD_in_LLMNR_prac1.png]]

3. Attacker gains the hash of password and username of client:
![[AD_in_LLMNR_prac3.png]]

4. Cracking this hash with hashcat:
**Running in kali linux**
```python
┌──(hyok㉿kali)-[~]
└─$ hashcat -m 5600 ntlmhash.txt /usr/share/wordlists/rockyou.txt --force
```
`--force` --> to force the hashcat to use gpu of base system
`-m 5600` --> to tell the hashcat to use **ntlmv2** method.
`/usr/share/wordlists/rockyou.txt` --> path to wordlists
`ntlmhash.txt` --> hash of step 3 
**plaintext of hash**
![[AD_in_LLMNR_prac4_1.png]]

**Running in windows and it is recommended to run in windows(base system to utilize gpu ruther than cpu)**
![[AD_in_LLMNR_prac_4_2.png]]

## LLMNR Defense:
![[AD_in_LLMNR_defense1.png]]