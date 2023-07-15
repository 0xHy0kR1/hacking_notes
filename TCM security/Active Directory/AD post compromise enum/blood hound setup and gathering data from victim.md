1. Installing blood hound
```python
apt install bloodhound
```

2. Bloodhound runs on tool called neo4j(setting up neo4j)
![[bloodhound1.png]]

3. Type `bloodhound` in the terminal to access the database

## Gathering data from victim using bloodhound
**Run the below commands**
1. powershell -ep bypass
2. . .\\SharpHound.ps1
3. Invoke-BloodHound -CollectionMethod All -Domain MARVEL.local -ZipFileName file.zip --> To copy domain controller data into a file named file.zip

**Note** - First download **SharpHound.ps1** in victim before doing above steps.