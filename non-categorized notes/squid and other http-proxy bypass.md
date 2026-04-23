### this is the way it should be used to bypass http-proxy sites
==_read carefully as ports might be different from the one you have. 
If you don't understand, just visit [Squid](6-%20Zettelkasten/Squid.md) and read it before you proceed._==






 we will first download Spose
```powershell
git clone https://github.com/aancw/spose.git
```

after that we need to 
```powershell
cd spose
```
then we run the script 
```powershell
python3 spose.py --proxy http://<% tp.frontmatter["RHOSTS"] %>:3128 --target <% tp.frontmatter["RHOSTS"] %>
```

we will get the following results 
![600](Assets/Pasted%20image%2020250720014520.png)
so we now know that 3306 and 8080 are open.
next, we need to setup the proxy in foxyproxy extension 
![300](Assets/Pasted%20image%2020250720014648.png)
![600](Assets/Pasted%20image%2020250720014704.png)
![600](Assets/Pasted%20image%2020250720014719.png)
![600](Assets/Pasted%20image%2020250720014735.png)
add all info and click save 
![600](Assets/Pasted%20image%2020250720014818.png)
select squid 
![600](Assets/Pasted%20image%2020250720014847.png)
then we can navigate to the website using 127.0.0.1:8080 
![1500](Assets/Pasted%20image%2020250720014944.png)
we got it.
next we need to check everything with a proxy. 

## 2- Run directory and file enumeration using tools like gobuster or dirb or dirsearch: 
```powershell
dirsearch -u http://127.0.0.1:8080 --proxy <% tp.frontmatter["RHOSTS"] %>:3128  -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --exclude-status 401,302,500
```