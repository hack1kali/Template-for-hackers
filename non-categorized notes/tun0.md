
[[tun0]] IP address
```powershell
ifconfig tun0 | grep -oP 'inet\s+\K[\d.]+' | head -n1
```



