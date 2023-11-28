## SMTP Introduction
- SMTP default port is 25.
- SMTP stands for "Simple Mail Transfer Protocol".
- In order to support email services, a protocol pair is required, comprising of SMTP and POP/IMAP.
- Together they allow the user to send outgoing mail and retrieve incoming mail, respectively.

**The SMTP server performs three basic functions:**
-  It verifies who is sending emails through the SMTP server.
-  It sends the outgoing mail
-  If the outgoing mail can't be delivered it sends the message back to the sender

Most people will have encountered SMTP when configuring a new email address on some third-party email clients, such as Thunderbird.
as when you configure a new email client, you will need to configure the SMTP server configuration in order to send outgoing emails.

## POP and IMAP:
- POP, or "Post Office Protocol" and IMAP, "Internet Message Access Protocol" are both email protocols who are responsible for the transfer of email between a client and a mail server.

## POP vs IMAP:
#### Email Retrieval:
1. POP:
	- When you use POP, your email client retrieves emails from the mail server and typically deletes them from the server and your email client becomes the primary storage location for your emails.
2. IMAP:
	- With IMAP, your email client syncs with the mail server, allowing you to access your emails from multiple devices. it means, that It keeps your emails stored on the server.

#### Synchronization:
1. POP:
	- POP does not synchronize your email client with the server.
2. IMAP:
	- IMAP provides synchronization capabilities.

#### Offline Access:
1. POP:
	- Since emails are downloaded to the local device, you can access them even without an internet connection.
2. IMAP:
	- IMAP requires an internet connection to access and synchronize emails since it interacts with the server.

## Components of SMTP:

**The figure shows the following five steps that an email needs to go through to reach the recipient’s inbox:**
1. A Mail User Agent (MUA), or simply an email client, has an email message to be sent. The MUA connects to a Mail Submission Agent (MSA) to send its message.
2. The MSA receives the message, checks for any errors before transferring it to the Mail Transfer Agent (MTA) server, commonly hosted on the same server.
3. The MTA will send the email message to the MTA of the recipient. The MTA can also function as a Mail Submission Agent (MSA).
4. A typical setup would have the MTA server also functioning as a Mail Delivery Agent (MDA).
5. The recipient will collect its email from the MDA using their email client.

**If the above steps sound confusing, consider the following analogy:**
1. You (MUA) want to send postal mail.
2. The post office employee (MSA) checks the postal mail for any issues before your local post office (MTA) accepts it.
3. The local post office checks the mail destination and sends it to the post office (MTA) in the correct country.
4. The post office (MTA) delivers the mail to the recipient mailbox (MDA).
5. The recipient (MUA) regularly checks the mailbox for new mail. They notice the new mail, and they take it.


![[SMTP5.png]]

1. **Mail User Agent (MUA):**
	- It is a computer application that helps you in sending and retrieving mail.
	- It is responsible for creating email messages to transfer to the mail transfer agent(MTA).

2. **Mail Transfer Agent(MTA)**
	- It is basically software that has the work to transfer mail from one system to another with the help of SMTP.

3. **Mail Submission Agent (MSA):**
	- It is a computer program that basically receives mail from a Mail User Agent(MUA) and interacts with the Mail Transfer Agent(MTA) for the transfer of the mail.

4. **Mail Delivery Agent(MDA):**
	- It is basically a system that helps in the delivery of mail to the local system.


## Working of SMTP
![[SMTP1.png]]

1. The mail user agent, which is either your email client or an external program. connects to the SMTP server of your domain, e.g. smtp.google.com. This initiates the SMTP handshake. This connection works over the SMTP port- which is usually 25. Once these connections have been made and validated, the SMTP session starts.
2. The process of sending mail can now begin. The client first submits the sender, and recipient's email address- the body of the email and any attachments, to the server.
3. The SMTP server then checks whether the domain name of the recipient and the sender is the same.
4. The SMTP server of the sender will make a connection to the recipient's SMTP server before relaying the email. If the recipient's server can't be accessed, or is not available- the Email gets put into an SMTP queue.
5. Then, the recipient's SMTP server will verify the incoming email. It does this by checking if the domain and user name have been recognised. The server will then forward the email to the POP or IMAP server.
6. The E-Mail will then show up in the recipient's inbox.


**Note** - 
   - imple Mail Transfer Protocol (SMTP) is used to communicate with an MTA server.
   - Because SMTP uses cleartext, where all commands are sent without encryption, we can use a basic Telnet client to connect to an SMTP server and act as an email client (MUA) sending a message.

### Connecting SMTP server with Telnet
![[SMTP6.png]]
   - Once connected, we issue `helo hostname` and then start typing our email.
   - After `helo`, we issue `mail from:`, `rcpt to:` to indicate the sender and the recipient.
   - When we send our email message, we issue the command `data` and type our message.
   - We issue `<CR><LF>.<CR><LF>` (or `Enter . Enter` to put it in simpler terms).
