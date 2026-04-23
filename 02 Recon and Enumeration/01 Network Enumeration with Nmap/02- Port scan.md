**NMAP TCP ports SCAN**
```powershell
sudo grc rustscan --ulimit 5000 -a <% tp.frontmatter["RHOSTS"] %> |tee rustscan.txt
# no ping option for windows like machines 
sudo grc rustscan --ulimit 5000 -a <% tp.frontmatter["RHOSTS"] %> -- -Pn |tee rustscan.txt
```
results 
```powershell

```

**Double checked with nmap**
```powershell
# add --Pn if you are not getting any results
grc nmap -p- --min-rate 5000 <% tp.frontmatter["RHOSTS"] %>

```
results 
```powershell

```

scanning with specific ports
```powershell
# no need to change anything here. just make sure the port list is correct
ports=$(cat rustscan.txt |grep '^Open ' |sed -e 's/^.*://g' |sort -n |tr '\n' ',' |sed 's/,$//')
# check if ports extracted correctly
echo $ports
grc nmap -p$ports -sC -sV -sT -n -A -T4 -Pn --open -oN nmap.out <% tp.frontmatter["RHOSTS"] %>
```
results 
```powershell

```


**(final double check)**
```powershell
sudo grc nmap -p- -oA tcp <% tp.frontmatter["RHOSTS"] %>
```
results 
```powershell

```

**UDP ports scan**
```powershell
# UDP fast scan (top 100)
sudo grc nmap -n -v -sU -F -T4 --reason --open -T4 -oA udp-fast <% tp.frontmatter["RHOSTS"] %> -Pn
```
results 
```powershell

```


```powershell
# top 20 UDP ports
sudo grc nmap -n -v -sU -T4 --top-ports=20 --reason --open -oA udp-top20 <% tp.frontmatter["RHOSTS"] %> -Pn
```
results 
```powershell

```


 ## automated 
```powershell
 #!/bin/bash

IP="<% tp.frontmatter["RHOSTS"] %>"   

echo "[+] Running RustScan 1 (no ping)"
sudo grc rustscan --ulimit 5000 -a $IP | tee rust1.txt

echo "[+] Running RustScan 2 (-Pn)"
sudo grc rustscan --ulimit 5000 -a $IP -- -Pn | tee rust2.txt

echo "[+] Extracting ports from RustScan"
ports1=$(grep '^Open ' rust1.txt | sed -e 's/^.*://g' | sort -n | tr '\n' ',' | sed 's/,$//')
ports2=$(grep '^Open ' rust2.txt | sed -e 's/^.*://g' | sort -n | tr '\n' ',' | sed 's/,$//')

echo "[+] Ports from run1: $ports1"
echo "[+] Ports from run2: $ports2"

# Compare
if [ "$ports1" == "$ports2" ]; then
    echo "[+] Ports match between RustScan 1 and 2 ✓"
else
    echo "[!] Ports differ between RustScan scans ✗"
fi

echo "[+] Running Nmap full TCP quick scan"
grc nmap -p- --min-rate 5000 $IP -oN nmap_p_full.txt

echo "[+] Extracting ports from Nmap full scan"
portsNmap=$(grep '/tcp' nmap_p_full.txt | grep open | cut -d'/' -f1 | tr '\n' ',' | sed 's/,$//')

echo "[+] Ports from Nmap: $portsNmap"

# Compare with rustscan
if [ "$portsNmap" == "$ports1" ]; then
    echo "[+] RustScan == Nmap ports ✓"
else
    echo "[!] RustScan != Nmap ports ✗"
fi

echo "[+] Running specific-port Nmap scan (-sC -sV)"
grc nmap -p$portsNmap -sC -sV -sT -n -A -T4 -Pn --open -oN nmap_detailed.txt $IP

echo "[+] Final double-check full TCP scan"
sudo grc nmap -p- -oA tcp_full $IP

echo "[+] Running UDP fast scan (top 100)"
sudo grc nmap -n -v -sU -F -T4 --reason --open -oA udp_fast $IP -Pn

echo "[+] Running UDP top 20 scan"
sudo grc nmap -n -v -sU -T4 --top-ports=20 --reason --open -oA udp_top20 $IP -Pn


echo ""
echo "------------------------------"
echo "        FINAL REPORT"
echo "------------------------------"
echo "RustScan ports run1:  $ports1"
echo "RustScan ports run2:  $ports2"
echo "Nmap ports:           $portsNmap"

echo ""
echo "Comparison summary:"
if [ "$ports1" == "$ports2" ]; then
    echo " ✓ RustScan 1 & 2 match"
else
    echo " ✗ RustScan 1 & 2 mismatch"
fi

if [ "$ports1" == "$portsNmap" ]; then
    echo " ✓ RustScan == Nmap"
else
    echo " ✗ RustScan != Nmap"
fi

echo ""
echo "[+] Scan completed."

 ```