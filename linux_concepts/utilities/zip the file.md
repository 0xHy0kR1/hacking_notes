   - ZIP is the most popular archive file format for compressing files and directories. Compressing files into an archived format helps conserve space and network bandwidth.
   - Even though the tape archive (tar) format is more common on [Linux](https://phoenixnap.com/glossary/what-is-linux) systems, ZIP is also used often due to its popularity.

## Check if zip Is Installed

   See whether the utility is available by checking the version:
```sh
zip --version
```

>**Install the zip and unzip utility with the following command:**
```sh
sudo apt install zip unzip
```


>**The general syntax for the "zip" command is:**
```sh
zip <options> <zip file> <source file(s)>
```
Without any options, the command creates a new ZIP file.

## zip Command Options

   The table below shows a short overview of the available options.
   ![[zip1.png]]
The zip command offers many other options you can view using the man command.

## Create a ZIP Archive

   The **`zip`** command, without any options, creates a new file. To test the command, do the following:
   
   1. Create files for archiving:
```sh
touch file{1..5}.txt   
```

   2. Use the **`zip`** command to archive the files:
```sh
zip files file1.txt file2.txt file3.txt file4.txt file5.txt
```
The command outputs the actions taken and creates a _files.zip_ archive.


## List ZIP File Contents

>**The "-sf" option lists the contents of a ZIP file. Provide only the ZIP file name, for example:**
```sh
zip -sf files.zip   
```


## Add Specific File Types to ZIP Archive

>To add only specific file types to a ZIP file, use a wildcard and provide the filetype extension.
```sh
zip files *.txt
```


## Add a Directory to ZIP Archive

> **Use the "-r" (recursive) option to add a directory to a ZIP file. For instance:**
```sh
zip -r files <directory>
```
The **`zip`** command adds the empty directory first, then populates it with the files.

## Delete Files From ZIP Archive

   1. To delete files from a ZIP archive, list the files from the archive using the **`-sf`** option first.
```sh
zip -sf <archive file>
```

   2. Locate the file for deletion and run **`zip`** with the **`-d`** tag:
```sh
zip -d <archive file> <files for deletion>
```

   For example:
```sh
zip -d files.zip file5.txt   
```
The command removes the specified files from the ZIP archive.


## Create and Encrypt ZIP File

>**A password protects the ZIP archive from extraction. To add password encryption to a ZIP file, use the "-e" option:**
```sh
zip -e <archive file> <files>   
```
The command starts a password entry prompt. After confirming, the files are added to the ZIP archive.


## Control ZIP Compression Level

   - The **`zip`** command allows controlling the compression level.
   - The ZIP file compression level and speed are reversely proportional. As the level increases, the compression takes longer.

>**To control the ZIP file compression level, use the following syntax:**
```sh
zip -<0-9> <archive file> <files>
```

**For example:**
```sh
zip -5 files *.txt
```

For the fastest compression, use "-1". For the highest level of compression, use **`-9`**.


## Create a ZIP Archive Using The GUI

   1. Open **Files** and navigate to the appropriate directory.

   2. Select the files for archiving, right-click the files, and choose **Compress**.
![[zip2.png]]

   3. Enter the archive name and choose the **.zip** format from the dropdown menu.
![[zip3.png]]
4. Click **Create** to create the ZIP file.