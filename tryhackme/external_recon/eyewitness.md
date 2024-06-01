- EyeWitness is an incredible tool that allows you to quickly get a feel for what assets to target first.
- We all know hundreds of content discovery tools that give us vast amounts of data, but do we ever focus on efficiently parsing all that data? How do you go through hundreds of endpoints? If you’re doing it manually, then EyeWitness may be of great help to you!

## What is EyeWitness?
- It’s goal is to help you efficiently assess what assets of your target to look into first.
- It achieves this by taking screenshots of every assets and showing you those screenshots alongside some header information and potential default credentials if applicable.

## Installing EyeWitness
```sh
sudo apt install eyewitness
```

## Uses

>Capturing screenshots of domains listed in the "domains.txt" file.
```sh
eyewitness -f domains.txt
```

After executing, the tool will open the result in your browser. Here you can assess the results. Let’s discuss them the screenshot below.
The result page starts off by giving us a nice overlay of all everything that it found. In this case we have Unauthorized pages, Not Found pages and Bad requests already filtered out of all the rest.
Scrolling down, we find screenshots and the headers of all these pages. We can now quickly assess which page we would like to target first!

![[eyewitness1.webp]]

## Features
![[eyewitness2.webp]]

### Input options
These are the options that can help you input the targets to take screenshots of.

>Line-separated file containing URLs to capture. As seen in the example above.
```sh
-f Filename
```

>Nmap XML or .Nessus file because yes, this tool can parse that output!
```sh
-x Filename.xml
```

>Single URL/Host to capture. If for some reason you’d only want to scan a single target.
```sh
--no-dns
```
![[eyewitness3.webp]]

