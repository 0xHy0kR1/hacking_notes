**Step 1: Checking System Requirements:**

Before proceeding with the installation, it’s essential to ensure that you have **go language 1.17 (go1.17) or above (latest)** is installed on your system.  
Verify your go lang installation by running below command:

```sh
go version
```

**Step 2: Downloading/Installing the GF Tool:**
```sh
 go install github.com/tomnomnom/gf@latest
```

**Step 3: Configuring the GF Tool:**
```sh
sudo cp ~/go/bin/gf /bin/
mkdir .gf 
mv ~/Gf-Patterns/*.json ~/.gf
```

**Step 4: Verifying the Installation:**
```sh
gf -list
```

**Step 5: Using the GF Tool:**
Now that you have the GF tool installed, let’s explore some basic usage examples:

**_Search for a specific pattern within a file:_**
```sh
cat file_with_para.txt | gf [ssrf,etc.]
```
