- Workspaces in Metasploit are used to separate datasets, allowing you to stay organized.
- It is a good idea to create a new workspace to organize all your collected data before starting a new penetration test.

## 1. The default workspace is selected when connecting to the database, which is represented by the * character before its name:
```python
msf > workspace
```

## 2. To display the usage for the workspace command, use the -h option as follows:
```python
msf > workspace -h
```

## 3. To add a new workspace, use the -a option followed by the name of the workspace:
```python
msf > workspace -a book
```

## 4. To list the available workspaces, simply type the workspace command:
```python
msf > workspace
```

## 5. To delete a workspace, use the -d option followed by the name of the workspace:
```python
msf > workspace -d book
```

## 6. To change the current workspace, use the workspace command followed by the name of the workspace you want to change to:
```python
msf > workspace book
```

## 7. To rename a workspace, use the workspace command with the -r option followed by the old workspace name and the new workspace name:
```python
msf > workspace -r book metasploit
```
