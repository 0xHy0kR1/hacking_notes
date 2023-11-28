- Internet Message Access Protocol (IMAP) is more sophisticated than POP3.
- IMAP makes it possible to keep your email synchronized across multiple devices (and mail clients). In other words, if you mark an email message as read when checking your email on your smartphone, the change will be saved on the IMAP server (MDA) and replicated on your laptop when you synchronize your inbox.

### Example - 
   - In the console output below, we use Telnet to connect to the IMAP server’s default port, and then we authenticate using `LOGIN username password`.
   - IMAP requires each command to be preceded by a random string to be able to track the reply. So we added `c1`, then `c2`, and so on.
   - Then we listed our mail folders using `LIST "" "*"`, before checking if we have any new messages in the inbox using `EXAMINE INBOX`.
     ![[IMAP1.png]]
     It is clear that IMAP sends the login credentials in cleartext, as we can see in the command `LOGIN frank D2xc9CgD`.