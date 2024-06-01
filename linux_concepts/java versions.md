Apt-get won't overwrite the existing java versions.

To switch between installed java versions, use the `update-java-alternatives` command.

**List all java versions:**
```java
update-java-alternatives --list
```

**Set java version as default (needs root permissions):**
```java
sudo update-java-alternatives --set /path/to/java/version
```
...where `/path/to/java/version` is one of those listed by the previous command (e.g. `/usr/lib/jvm/java-7-openjdk-amd64`).

**Additional information:**
`update-java-alternatives` is a convenience tool that uses Debian's [alternatives system](https://wiki.debian.org/DebianAlternatives) (`update-alternatives`) to set a bunch of links to the specified java version (e.g. `java`, `javac`, ...).

## Install OpenJDK on linux
   - To install OpenJDK from a `.tar.gz` file on Linux, you can follow these general steps.
   - Replace the file name with the appropriate version if needed.

1. **Download the OpenJDK Archive:**
	- Go to the official OpenJDK website or a trusted source and download the `.tar.gz` file for the desired version.

2. **Move to the directory that you want to extract the openjdk8:**
```sh
cd /usr/lib/jvm
```

3. **Extract the jdk there**
```sh
sudo tar -xvzf ~/Downloads/jdk-8u202-linux-x64.tar.gz
```

4. **Go inside the newly created directory using cd command**
```sh
cd jdk1.8.0_202
/usr/lib/jvm/jdk1.8.0_202
```

5. **Now, set the above openjdk path to the environment**
![[java_version1.png]]

6. **Now, we need to install jdk on our alternatives as well so that we can switch between different java versions
```sh
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.8.0_202/bin/java" 0
```

```sh
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.8.0_202/bin/javac" 0
```

7. **Now, we need to set the java and java interpreter in the alternatives**
```sh
sudo update-alternatives --set java /usr/lib/jvm/jdk1.8.0_202/bin/java   
```

```sh
sudo update-alternatives --set java /usr/lib/jvm/jdk1.8.0_202/bin/javac
```

8. **Switch between different java versions using the below command**
```sh
sudo update-alternatives --config java
```

![[java_version2.png]]
