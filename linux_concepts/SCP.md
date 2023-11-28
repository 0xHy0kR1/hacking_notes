**SCP** command is used to copy file(s) between servers in a secure way.

>Basic Syntax of SCP Command
```shell
scp source_file_name username@destination_host:destination_folder
```
Above command will read as copy “**source_file_name**” into “**destination_folder**” at “**destination_host**” using the “**username**” account.
It will copy the files in the background.


>Copy File From Local Host to Remote Server
```shell
scp -v scp-cheatsheet.pdf tecmint@192.168.0.183:/home/tecmint/
```
You can use the “`-v`” parameter to print debug information into the screen.

**Sample Output**:
![[SCP1.png]]


>Copy File From Remote Host to Local Host
```shell
scp -v tecmint@192.168.0.183:/home/ravi/ssh-cheatsheet.pdf /home/tecmint/.
```
The following command copies a file “**ssh-cheatsheet.pdf**” from a remote host to a local system under **/home/tecmint** directory.

**Sample output:**
![[SCP2.png]]


>Copy File From Remote Host to Another Host
```shell
scp -v tecmint@192.168.0.183:/home/ravi/ssh-cheatsheet.pdf tecmint@192.168.0.102:/home/anusha/.
```
The following command copies a file “**ssh-cheatsheet.pdf**” from a remote host to another remote host system under **/home/tecmint** directory.


>Copy Files with Original Creation Date and Time
```shell
scp -p scp-cheatsheet.pdf tecmint@192.168.0.183:/home/tecmint/.
```
The “`-p`” parameter will preserve files’ original modification and access times while copying files along with the estimated time and the connection speed will appear on the screen.

