

1- convert target file to hash 
```powershell
zip2john sitebackup3.zip > hash
```

2- crack it 
```powershell
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```
3- unzip it 
```powershell
7z x sitebackup3.zip
```
and enter password you got 

4- grep passwords or secret 
```powershell
grep -rinE '(password|username|user|pass|key|token|secret|admin|login|credentials)' .
```

* try the found secret not only with root but with different other users that can do ssh 