	1. Install Go (if not already installed):
```sh
sudo apt update
sudo apt install golang
```

2. Install `assetfinder` using `go install`:
```sh
go install github.com/tomnomnom/assetfinder@latest
```

3. Copy assetfinder binary to /bin/ as follows:
```sh
┌──(kali㉿kali)-[~/go/bin]
└─$ sudo cp assetfinder /bin/
```

4. Verify the installation:
```sh
assetfinder --help
```

# Testing and Results
```sh
./assetfinder [--subs-only] <domain>
```

>For example, to find both subdomains and domains associated with GE.com, use:
```sh
root@Ubuntu ~ # ./assetfinder ge.com
blizzard000.ge.com
blizzard00.ge.com
ns0.ge.com
milan1-1.ge.com
milan2-1.ge.com
na2001.ge.com
crpeomusanyca01.ge.com
corpuwb01.ge.com
consind01.ge.com
blizzard01.ge.com
....
...
..
```
