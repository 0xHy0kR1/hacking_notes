## HTTP Path put - 
- The `scanner/http/http_put` module is a scanner auxiliary module that allows you to test for HTTP PUT file upload vulnerability on a target web server.
- It sends a specially crafted HTTP PUT request to the target server with a file to be uploaded, and then checks whether the file has been uploaded successfully.
# Code - 
```python
msf6 > use auxiliary/scanner/http/http_put
msf6 auxiliary(scanner/http/http_put) > set PATH /uploads
PATH => /uploads
msf6 auxiliary(scanner/http/http_put) > set RPORT 8585
RPORT => 8585
msf6 auxiliary(scanner/http/http_put) > set RHOSTS 192.168.216.11
RHOSTS => 192.168.216.11
msf6 auxiliary(scanner/http/http_put) > run

[+] File uploaded: http://192.168.216.11:8585/uploads/msf_http_put_test.txt
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

```
# Some extra information - 
![[http_put_vulnerability.jpeg]]