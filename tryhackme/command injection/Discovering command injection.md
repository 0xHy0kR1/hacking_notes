- This vulnerability exists because applications often use functions in programming languages such as PHP, Python and NodeJS to pass data to and to make system calls on the machine’s operating system.
- In this code snippet, the application takes data that a user enters in an input field named `$title` to search a directory for a song title.
![[ci1.png]]
1. The application stores MP3 files in a directory contained on the operating system.

2. The user inputs the song title they wish to search for. The application stores this input into the `$title` variable.

3. The data within this `$title` variable is passed to the command `grep` to search a text file named _songtitle.__txt_ for the entry of whatever the user wishes to search for.

4. The output of this search of _songtitle.__txt_ will determine whether the application informs the user that the song exists or not.

Now, this sort of information would typically be stored in a database; however, this is just an example of where an application takes input from a user to interact with the application’s operating system.

**An attacker could abuse this application by injecting their own commands. they could ask the application to read data from a more sensitive file.**


























