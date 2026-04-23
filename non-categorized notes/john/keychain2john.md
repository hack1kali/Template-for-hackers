
here we need to convert keychain2john and use that to login 
```powershell
keychain2john filename.keychain-db > hash
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