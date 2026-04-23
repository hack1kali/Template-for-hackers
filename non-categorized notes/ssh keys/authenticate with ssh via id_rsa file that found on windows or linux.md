Are you able to upload files to user folder? if yes, check [generate .ssh keys](5-%20Templates/non-categorized%20notes/ssh%20keys/generate%20.ssh%20keys.md) directly

### File lactation
#### windows 
```powershell
C:\Users\User-Name\.ssh\id_rsa
```

### save file to linux 
Make a new folder 
```powershell
mkdir .ssh
```
change permissions of folder to 700
```powershell
chmod 700 .ssh
```
make a file and save the id_rsa key to it 
```powershell
subl .ssh/id_rsa
```
it should be ended with a new empty line 
![600](Assets/Pasted%20image%2020250719180439.png)
change permissions
```powershell
chmod 600 .ssh/id_rsa
```
### connect
```powershell
ssh -i .ssh/id_rsa <user-name>@<% tp.frontmatter["RHOSTS"] %>
```

### common errors
![600](Assets/Pasted%20image%2020250719180645.png)
just add a new line to the file and it will be solved as explained above
