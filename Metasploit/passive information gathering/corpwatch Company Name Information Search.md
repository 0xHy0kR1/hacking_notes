This module interfaces with the CorpWatch API to get publicly available info for a given company name.
# code - 
```python
msf6 auxiliary(gather/corpwatch_lookup_name) > set COMPANY_NAME google
COMPANY_NAME => google
msf6 auxiliary(gather/corpwatch_lookup_name) > run
 
[*] Company Information
---------------------------------
[*] CorpWatch (cw) ID): cw_929214
[*] Company Name: CapitalG LP
[*] Address: 1600 AMPITHEATRE PARKWAY, MOUNTAIN VIEW CA 94043
[*] Sector: 
[*] Industry: 
[*] Company Information
---------------------------------
[*] CorpWatch (cw) ID): cw_1186584
[*] Company Name: Google LLC
[*] Address: 1600 AMPHITHEATRE PARKWAY, MOUNTAIN VIEW CA 94043
[*] Sector: 
[*] Industry: 
[*] Company Information
---------------------------------
[*] CorpWatch (cw) ID): cw_111030
[*] Company Name: Google LLC
[*] Address: Delaware
[*] Sector: 
[*] Industry: 
[*] Auxiliary module execution completed

```
