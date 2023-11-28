- Post Office Protocol version 3 (POP3) is a protocol used to download the email messages from a Mail Delivery Agent (MDA) server, as shown in the figure below.
- The mail client connects to the POP3 server, authenticates, downloads the new email messages before (optionally) deleting them.
  ![[pop3_1.png]]

#### Example
**The example below shows what a POP3 session would look like if conducted via a Telnet client.**
   - First, the user connects to the POP3 server at the POP3 default port 110.
   - Authentication is required to access the email messages; the user authenticates by providing his username `USER frank` and password `PASS D2xc9CgD`.
   - Using the command `STAT`, we get the reply `+OK 1 179`;
   - based on [RFC 1939](https://datatracker.ietf.org/doc/html/rfc1939), a positive response to `STAT` has the format `+OK nn mm`, where _nn_ is the number of email messages in the inbox, and _mm_ is the size of the inbox in octets (byte).
   - The command `LIST` provided a list of new messages on the server, and `RETR 1` retrieved the first message in the list.
     ![[pop3_2.png]]
     - In general, your mail client (MUA) will connect to the POP3 server (MDA), authenticate, and download the messages.
     - Based on the default settings, the mail client deletes the mail message after it downloads it.
     - To keep all mailboxes synchronized, we need to consider other protocols, such as IMAP.

