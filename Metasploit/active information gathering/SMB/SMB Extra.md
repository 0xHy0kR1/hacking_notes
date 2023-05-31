- Metasploit has a plethora of SMB auxiliary modules that you should try. To list all the available SMB modules, you can hit Tab button to display all the available modules under auxiliary/scanner/smb/:
```python
msf > use auxiliary/scanner/smb/ ... use auxiliary/scanner/smb/smb_ms17_010 use auxiliary/scanner/smb/smb_uninit_cred use auxiliary/scanner/smb/smb_version msf > use auxiliary/scanner/smb/
```