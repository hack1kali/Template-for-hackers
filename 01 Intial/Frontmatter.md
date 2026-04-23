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



#### if the machine does not behave as expected, please execute the following command 
```css
sudo ip link set dev tun0 mtu 800
Make sure to wait 2-3 minuts after lunching the machine, otherwise, the lab will get corrupted!!!!
```

## kali side
#### start onedrive
```powershell
#sudo apt remove onedrive
#sudo apt install onedrive
onedrive --monitor
```

#### start obsidian
```powershell
obsidian
```
# remove it later  ---------------------------------


#### Initial Access

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity:** **Critical**

**Steps to reproduce the attack:**
#### Service Enumeration
The service enumeration portion of a penetration test focuses on gathering information about what services are alive on a system or systems.
This is valuable for an attacker as it provides detailed information on potential attack vectors into a system.
Understanding what applications are running on the system gives an attacker needed information before performing the actual penetration test.
In some cases, some ports may not be listed.

**Port Scan Results**

| Server IP Address | Ports Open          |
| ----------------- | ------------------- |
| 192.168.x.x       | **TCP**: 1433,3389\ |
|                   | **UDP**: 1434,161   |

**Nmap Scan Results:**

#### Initial access - (Anonymous SMB share leads to Wordpress RCE)


**Proof of Concept Code Here:**

**Local.txt Proof Screenshot**

**Local.txt Contents**
windows
```powershell
whoami && ipconfig && type c:\Users\<user>\Desktop\local.txt && hostname
```
linux
```powershell
id && ip a && cat /home/<user>/local.txt && hostname
```

is it interactive shell? 
try `/bin/bash -p`


#### Privilege Escalation

*Additional Priv Esc info*

**Vulnerability Exploited:**

**Vulnerability Explanation:**

**Vulnerability Fix:**

**Severity:**

**Exploit Code:**

**Proof Screenshot Here:**

windows
```powershell
whoami && ipconfig && type c:\Users\Administrator\Desktop\proof.txt && hostname
```

linux
```powershell
id && ip a && cat /root/proof.txt && hostname
```
is it interactive shell? 
try `/bin/bash -p
#### 5- Post-Exploitation


