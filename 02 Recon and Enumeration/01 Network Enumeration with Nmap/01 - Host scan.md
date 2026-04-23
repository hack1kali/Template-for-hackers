## Initial Nmap Scan

# ARP scan
```powershell
sudo grc nmap -PR -sn <% tp.frontmatter["Subnet"] %>/24
```


# bash handy script
```powershell
#!/bin/bash
addr=${1:-<% tp.frontmatter["Subnet"] %>}
subnet="${addr%.*}"
for i in {1..254}; do
  host="$subnet.$i"
  ping -c1 -w1 $subnet.$i >& /dev/null && echo "$host UP ++++" || echo "$host down" &
  sleep 0.1 || break  # lets you Ctrl+C out of loop
done
wait $(jobs -rp)
echo "Done"
```

