# code - 
```python
msf > db_nmap -Pn -sTV -T4 --open --min-parallelism 64 --version-all 192.168.216.10 -p -
```

## Information to the above - 
- We use db_nmap with the -Pn option to treat all hosts as online and skip host discovery.
- - sTV to perform a TCP connect scan. the V flag to carry out a version scan of the open ports discovered.
- -T4 to set the timing template higher so the scan runs faster.
- The -- open option will only show open ports.
- --min-parallelism is used to specify the minimum amount of parallel processes at one time.
- --version-all to try every single probe in order to identify a more specific version of the service running on an open port.
- To run the scan, we set the IP address of the target host and use -p - to specify that we want to scan all the 65535 ports.