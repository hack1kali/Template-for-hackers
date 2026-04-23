
1- generate keys
```powershell
ssh-keygen
```

![600](Assets/Pasted%20image%2020250811003603.png)
2-copy the output public file to the current directory 
```powershell
cp /root/.ssh/id_ed25519.pub .
```
3-rename it 
```powershell
mv id_ed25519.pub authorized_keys
```
4-upload it to `/home/username/.ssh`
5- change permission of the other file 
```powershell
chmod 600 /root/.ssh/id_ed25519
```

6- ssh to the server
```powershell
ssh -i /root/.ssh/id_ed25519 <user-name>@<% tp.frontmatter["RHOSTS"] %>
```