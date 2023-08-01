## Introduction
The WPScan framework is capable of enumerating & researching a few security vulnerability categories present in WordPress sites - including - but not limited to:
- Sensitive Information Disclosure (Plugin & Theme installation versions for disclosed vulnerabilities or CVE's)
- Path Discovery (Looking for misconfigured file permissions i.e. wp-config.php)
- Weak Password Policies (Password bruteforcing)
- Presence of Default Installation (Looking for default files)
- Testing Web Application Firewalls (Common WAF plugins)

### Installing WPScan
```python
sudo apt update && sudo apt install wpscan
```

**Note** - Updata local database before performing any scans.
```python
wpscan --update
```

## WPScan modes

### Enumerating for Installed Themes
- WPScan has a few methods of determining the active theme on a running WordPress installation.
- Using the "Network" tab in your web browsers developer tools, you can see what files are loaded when you visit a webpage.
![[web_enum5.png]]

- We can take a pretty good guess that the name of the current theme is "twentytwentyone". After inspecting the source code of the website, we can note additional references to "twentytwentyone".
![[web_enum6.png]]

- Now, using WPScan to speed this process up by using the `--enumerate` flag with the `t` argument like so:
```python
wpscan --url http://cmnatics.playground/ --enumerate t
```
After a couple of minutes, we can begin to see some results:
![[web_enum7.png]]
The great thing about WPScan is that the tool lets you know how it determined the results it has got. 
In this case, we're told that the "twentytwenty" theme was confirmed by scanning "_Known Locations_". The "twentytwenty" theme is the default WordPress theme for WordPress versions in 2020.

## Enumerating for Installed Plugins
Since plugins will all be located in /wp-content/plugins/pluginname, WPScan can enumerate for common/known plugins.
- WPScan uses additional methods to discover plugins (such as looking for references or embeds on pages for plugin assets).
- We can use the `--enumerate` flag with the `p` argument like so:
```python
wpscan --url http://cmnatics.playground/ --enumerate p
```

**Note** - 
1. plugins must have a "README.txt" file. This file contains meta-information such as the plugin name, the versions of WordPress it is compatible with and a description.

## Enumerating for Users
- WPScan is capable of performing brute-forcing attacks.
- WordPress sites use authors for posts. Authors are in fact a type of user.
![[web_enum9.png]]
- This scan was performed by using the `--enumerate` flag with the `u` argument like so:
```python
wpscan --url http://cmnatics.playground/ --enumerate u
```

## The "Vulnerable" Flag
- In the commands so far, we have only enumerated WordPress to discover what themes, plugins and users are present.
- At the moment, we'd have to look at the output and use sites such as MITRE, NVD and CVEDetails to look up the names of these plugins and the version numbers to determine any vulnerabilities.
- WPScan has the `v` argument for the `--enumerate` flag alongside another (such as `p` for plugins).
**Example** - 
**our syntax would like so:**
```python
wpscan --url http://cmnatics.playground/ --enumerate vp
```

**Note** - this requires setting up WPScan to use the WPVulnDB API

## Performing a Password Attack
we use the output of our username enumeration to build a command like so:
```python
wpscan --url http://cmnatics.playground /usr/share/wordlists/rockyou.txt --usernames phreakazoid
```

## Adjusting WPScan's Aggressiveness (WAF)
- Lots of requests to a web server can trigger things such as firewalls and ultimately result in you being blocked by the server.
- This means that some plugins and themes may be missed by our WPScan. we can use arguments such as `--plugins-detection` and an aggressiveness profile (passive/aggressive).
**Example** - 
```python
--plugins-detection aggressive
```

# Summary - Cheatsheet
![[web_enum10.png]]