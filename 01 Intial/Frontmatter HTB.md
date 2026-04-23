---
RHOSTS:
LHOST:
VHOST:
MS01-RHOST-internal:
MS02-RHOST:
DC01-RHOST:
Subnet:
domain-username:
domain-password:
domain-password-hash:
---

# remove it later  ---------------------------------

```powershell
RHOSTS:  the ip you are currently attacking 
LHOST:  your tun0 IP
VHOST:  the domain name or the website name registered at /etc/hosts
MS01-RHOST-internal: the private ip address within the internal machine like 10.10.71.141
MS02-RHOST: public IP like 10.10.71.142
DC01-RHOST: public IP like 10.10.71.140
Subnet: is the private network IP like 10.10.71.0/24 but without the /24
username: valid username
password: valid password
domain-password-hash: it is the hash of the password for the above username
```

lower MTU
```css
sudo ip link set dev tun0 mtu 1200
```


#### Initial Access


#### Service Enumeration



#### Initial access - 


**Proof of Concept Code Here:**

**Local.txt Proof Screenshot**

**Local.txt Contents**
windows
```powershell
whoami && ipconfig && type c:\Users\<user>\Desktop\user.txt && hostname
```
linux
```powershell
id && ip a && cat /home/<user>/user.txt && hostname
```

is it interactive shell? 
try `/bin/bash -p`


#### Privilege Escalation



windows
```powershell
whoami && ipconfig && type c:\Users\Administrator\Desktop\root.txt && hostname
```

linux
```powershell
id && ip a && cat /root/root.txt && hostname
```
is it interactive shell? 
try `/bin/bash -p
#### 5- Post-Exploitation


