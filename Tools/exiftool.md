- **ExifTool** is a free and open source software program which is used to read, write and update metadata of various types of files such as PDF, Audio, Video and images.
- It is platform independent, available as a perl library as well as a command line application.
- Metadata can be described as information about the data such as file size, date created, file type, etc.

#### Installing ExifTool
```shell
sudo apt-get install libimage-exiftool-perl
```


>**Extract information from a file**
```shell
exiftool a.jpg
```
A basic command to extract all metadata from a file named `a.jpg`.


>**Basic write example**
```shell
exiftool -artist=me a.jpg
```
Writes Artist tag to `a.jpg`. Since no group is specified, EXIF:Artist will be written and all other existing Artist tags will be updated with the new value ("`me`").


>**Write multiple files**
```shell
exiftool -artist=me a.jpg b.jpg c.jpg
```
Writes Artist tag to three image files.


>**Write to all files in a directory**
```shell
exiftool -artist=me c:/images
```
Writes Artist tag to all files in directory `c:/images`.


>**Write multiple tags**
```shell
exiftool -artist="Phil Harvey" -copyright="2011 Phil Harvey" a.jpg
```
Writes two tags to `a.jpg`.


>**Extracting duplicate tags**
```shell
exiftool -a -u -g1 a.jpg
```
Print all meta information in an image, including duplicate and unknown tags, sorted by group (for family 1).


>**Print common meta information for all images in dir.**
```shell
exiftool -common dir
```


>List meta information in tab-delimited column form for all images in directory `DIR` to an output text file named "out.txt".
```shell
exiftool -T -createdate -aperture -shutterspeed -iso DIR > out.txt
```


>Print ImageSize and ExposureTime tag names and values.
```shell
exiftool -s -ImageSize -ExposureTime b.jpg
```


>Print standard Canon information from two image files.
```shell
exiftool -l -canon c.jpg d.jpg
```


>Recursively extract common meta information from files in C directory, writing text output into files with the same names but with a C<.txt> extension.
```shell
exiftool -r -w .txt -common pictures
```


>**Extracting Location of the Image**
```shell
exiftool <file_name> | grep GPS
```
It will give us GPS coordinates of the location where the image was captured.

>Creating Thumbnail Image
```shell
exiftool -ThumbnailImage <file_name> > thumb.jpg
```
This will save the thumbnail of original image as “thumb.jpg” and this thumbnail will be lesser in size as compared to original image


>Extracting Metadata using Keywords
```shell
exiftool -”*width*” <file_name>
```
When we type above command, it will give us all the tags related to width


>Verbose Mode of ExifTool
```shell
exiftool -v <file_name>
```
Verbose mode of **ExifTool** gives us more details of the file as compared to normal mode.


>Removing Metadata of File
```shell
exiftool -all= <file_name>
```
When we type above command in terminal, not all but some metadata is removed.


**Note** - 
**ExifTool** is used not only with images, it can also be used to extract metadata of PDF and Video files too. The syntax to get metadata of PDF and Video files is same as that of images.

