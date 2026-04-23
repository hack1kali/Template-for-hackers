---
RHOSTS: 10.10.11.87
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
##### NMAP MS01
###### 1- TCP
```powershell
sudo grc rustscan --ulimit 5000 -a 10.10.11.87 |tee rustscan.txt
# no ping option for windows like machines 
sudo grc rustscan --ulimit 5000 -a 10.10.11.87 -- -Pn |tee rustscan.txt
```
results 
```powershell

```

**Double check with nmap**
```powershell
# add --Pn if you are not getting any results
grc nmap -p- --min-rate 5000 10.10.11.87

```
results 
```powershell

```

### with specific ports
```powershell
# no need to change anything here. just make sure the port list is correct
ports=$(cat rustscan.txt |grep '^Open ' |sed -e 's/^.*://g' |sort -n |tr '\n' ',' |sed 's/,$//')
# check if ports extracted correctly
echo $ports
grc nmap -p$ports -sC -sV -sT -n -A -T4 -Pn --open -oN nmap.out 10.10.11.87
```
results 
```powershell

```



```powershell
sudo grc nmap -p- -oA tcp 10.10.11.87
```
results 
```powershell

```

###### 2- UDP scan

```powershell
# UDP fast scan (top 100)
sudo grc nmap -n -v -sU -F -T4 --reason --open -T4 -oA udp-fast 10.10.11.87 -Pn
```
results 
```powershell

```


```powershell
# top 20 UDP ports
sudo grc nmap -n -v -sU -T4 --top-ports=20 --reason --open -oA udp-top20 10.10.11.87 -Pn
```
results 
```powershell

```


 
##### register the domain name and domain controller url as following 

![[Assets/Pasted image 20250429100308.png|400]]

2- add the IP with the domain name and the domain controller url to your /etc/hosts
![[Assets/Pasted image 20250429100400.png]]



###### finish ligolo-ng setup first 
##### NMAP MS02
###### 1- TCP
```powershell
sudo grc rustscan --ulimit 5000 -a null |tee rustscan.txt
# no ping option for windows like machines 
sudo grc rustscan --ulimit 5000 -a null -- -Pn |tee rustscan.txt
```
results 
```powershell

```

**Double check with nmap**
```powershell
# add --Pn if you are not getting any results
grc nmap -p- --min-rate 5000 null

```
results 
```powershell

```

### with specific ports
```powershell
# no need to change anything here. just make sure the port list is correct
ports=$(cat rustscan.txt |grep '^Open ' |sed -e 's/^.*://g' |sort -n |tr '\n' ',' |sed 's/,$//')
# check if ports extracted correctly
echo $ports
grc nmap -p$ports -sC -sV -sT -n -A -T4 -Pn --open -oN nmap.out null
```
results 
```powershell

```



```powershell
sudo grc nmap -p- -oA tcp null
```
results 
```powershell

```

###### 2- UDP scan

```powershell
# UDP fast scan (top 100)
sudo grc nmap -n -v -sU -F -T4 --reason --open -T4 -oA udp-fast null -Pn
```
results 
```powershell

```


```powershell
# top 20 UDP ports
sudo grc nmap -n -v -sU -T4 --top-ports=20 --reason --open -oA udp-top20 null -Pn
```
results 
```powershell

```


##### NMAP DC01
###### 1- TCP
```powershell
sudo grc rustscan --ulimit 5000 -a null |tee rustscan.txt
# no ping option for windows like machines 
sudo grc rustscan --ulimit 5000 -a null -- -Pn |tee rustscan.txt
```
results 
```powershell

```

**Double check with nmap**
```powershell
# add --Pn if you are not getting any results
grc nmap -p- --min-rate 5000 null

```
results 
```powershell

```

### with specific ports
```powershell
# no need to change anything here. just make sure the port list is correct
ports=$(cat rustscan.txt |grep '^Open ' |sed -e 's/^.*://g' |sort -n |tr '\n' ',' |sed 's/,$//')
# check if ports extracted correctly
echo $ports
grc nmap -p$ports -sC -sV -sT -n -A -T4 -Pn --open -oN nmap.out null
```
results 
```powershell

```



```powershell
sudo grc nmap -p- -oA tcp null
```
results 
```powershell

```

###### 2- UDP scan

```powershell
# UDP fast scan (top 100)
sudo grc nmap -n -v -sU -F -T4 --reason --open -T4 -oA udp-fast null -Pn
```
results 
```powershell

```


```powershell
# top 20 UDP ports
sudo grc nmap -n -v -sU -T4 --top-ports=20 --reason --open -oA udp-top20 null -Pn
```
results 
```powershell

```















