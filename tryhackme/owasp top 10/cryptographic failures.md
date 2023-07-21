## Introduction
- A **cryptographic failure** refers to any vulnerability arising from lack of use of cryptographic algorithms for protecting sensitive information.
- Web applications require cryptography to provide confidentiality for their users at many levels.

**Example** - 
When you are accessing your email account using your browser, you want to be sure that the communications between you and the server are encrypted. That way, any eavesdropper trying to capture your network packets won't be able to recover the content of your email addresses. When we encrypt the network traffic between the client and server, we usually refer to this as **encrypting data in transit**.
Since your emails are stored in some server managed by your provider, it is also desirable that the email provider can't read their client's emails. To this end, your emails might also be encrypted when stored on the servers. This is referred to as **encrypting data at rest**.

At more complex levels, taking advantage of some cryptographic failures often involves techniques such as "Man in The Middle Attacks", whereby the attacker would force user connections through a device they control.

## Introduction SQLite
- flat-file databases are stored as a file on the disk of a computer.
- The most common format of a flat-file database is an SQLite database.
- The client we used to interact with the SQLite database is `sqlite3` and is installed on many Linux distributions by default.

### Practicals with the SQLite database

1. From below, We can see that there is an SQLite database in the current folder.
![[owasp1.png]]

2. To access it, we use `sqlite3 <database-name>`:
![[owasp2.png]]

3. From here, we can see the tables in the database by using the `.tables` command:
![[owasp3.png]]

4. let's use `PRAGMA table_info(customers);` to see the table information. Then we'll use `SELECT * FROM customers;` to dump the information from the table:
![[owasp4.png]]
- We can see from the table information that there are four columns: `custID`, `custName`, `creditCard` and `password`.
- You may notice that this matches up with the results. Take a look in first row.

