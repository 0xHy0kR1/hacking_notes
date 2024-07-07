1. Check Current Shell:
```sh
echo $SHELL
```

2. Switch to Zsh:
- If you're not already using Zsh, you can switch to it by running:
```sh
zsh
```

3. Install Zsh (if necessary):
- If Zsh is not installed, you can install it using:
```sh
sudo apt install zsh
```

4. Set Zsh as Default Shell:
- To set Zsh as your default shell, use the `chsh` command:
```sh
chsh -s $(which zsh)
```

5. Copy and put the below script in "recon_scripts" file under "/bin/":
```sh
#!/bin/bash
#----- AWS -------

# Lists the contents of an S3 bucket
# Example usage: s3ls "my-bucket-name"
s3ls(){
    aws s3 ls s3://$1
}

# Copies a file to an S3 bucket
# Example usage: s3cp "my-bucket-name" "path/to/local/file"
s3cp(){
    aws s3 cp $2 s3://$1 
}

#---- Content discovery ----

# Extracts endpoints from an application.wadl file and appends them to yahooapi.txt
# Example usage: thewadl "http://example.com/application.wadl"
thewadl(){ 
    curl -s $1 | grep path | sed -n "s/.*resource path=\"\(.*\)\".*/\1/p" | tee -a ~/tools/dirsearch/db/yahooapi.txt
}

#----- recon -----

# Runs crtndstry tool for domain reconnaissance
# Example usage: crtndstry "example.com"
crtndstry(){
    ./tools/crtndstry/crtndstry $1
}

# Runs Amass passively, saves output to JSON, and probes the domains
# Example usage: am "example.com"
am(){ 
    amass enum --passive -d $1 -json $1.json
    jq .name $1.json | sed "s/\"//g" | httprobe -c 60 | tee -a $1-domains.txt
}

# Runs httprobe on all hosts from certspotter
# Example usage: certprobe "example.com"
certprobe(){ 
    curl -s https://crt.sh/\?q\=\%.$1\&output\=json | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u | httprobe | tee -a ./all.txt
}

# Runs masscan on specified ports
# Example usage: mscan "example.com"
mscan(){ 
    sudo masscan -p4443,2075,2076,6443,3868,3366,8443,8080,9443,9091,3000,8000,5900,8081,6000,10000,8181,3306,5000,4000,8888,5432,15672,9999,161,4044,7077,4040,9000,8089,443,7443
}

# Fetches DNS names from certspotter API and filters them
# Example usage: my_certspotter "example.com"
my_certspotter(){ 
    curl -s https://certspotter.com/api/v0/certs\?domain\=$1 | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | sort -u | grep $1
} #h/t Michiel Prins

# Fetches domain names from crt.sh and filters them
# Example usage: crtsh "example.com"
crtsh(){
    curl -s https://crt.sh/?Identity=%.$1 | grep ">*.$1" | sed 's/<[/]*[TB][DR]>/\n/g' | grep -vE "<|^[\*]*[\.]*$1" | sort -u | awk 'NF'
}

# Fetches DNS names from certspotter API and runs nmap on them
# Example usage: certnmap "example.com"
certnmap(){
    curl https://certspotter.com/api/v0/certs\?domain\=$1 | jq '.[].dns_names[]' | sed 's/\"//g' | sed 's/\*\.//g' | sort -u | grep $1 | nmap -T5 -Pn -sS -i - -oA $1-nmap
} #h/t Jobert Abma

# Fetches IP information using ipinfo.io API
# Example usage: ipinfo "8.8.8.8"
ipinfo(){
    curl http://ipinfo.io/$1
}

#------ Tools ------

# Runs dirsearch for directory brute-forcing
# Example usage: dirsearch "http://example.com" "php,html"
dirsearch(){ # runs dirsearch and takes host and extension as arguments
    python3 ~/tools/dirsearch/dirsearch.py -u $1 -e $2 -t 50 -b 
}

# Runs sqlmap for SQL injection testing
# Example usage: sqlmap "http://example.com/page?id=1"
sqlmap(){
    python ~/tools/sqlmap*/sqlmap.py -u $1 
}

# Sets up a netcat listener on a specified port
# Example usage: ncx "1234"
ncx(){
    nc -l -n -vv -p $1 -k
}

# Fetches domains from crt.sh, probes them, and runs dirsearch
# Example usage: crtshdirsearch "example.com" "php,html"
crtshdirsearch(){ 
    curl -s https://crt.sh/?q\=%.$1\&output\=json | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u | httprobe -c 50 | grep https | xargs -n1 -I{} python3 ~/tools/dirsearch/dirsearch.py -u {} -e $2 -t 50 -b 
}

```

6. Source .zshrc:
- Once you're in Zsh, you can source your `.zshrc` file:
```sh
source ~/.zshrc
```