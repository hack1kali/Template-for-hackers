

1- Conn to MSRPC (unauthenticated)
```powershell
rpcclient -U "" -N  <% tp.frontmatter["RHOSTS"] %>
```

2- Conn to MSRPC (authenticated)
```powershell
rpcclient -U "<% tp.frontmatter["domain-username"] %>%<% tp.frontmatter["domain-password"] %>" <% tp.frontmatter["RHOSTS"] %>
```

3- enumeration 
3.1 enum users
```powershell
enumdomusers
```

3.2 enum groups
```powershell
enumdomgroups
```



```python
# Get information about the DC
srvinfo

# Get information about objects such as groups (enum*)
enumdomains
enumdomgroups
enumalsgroups builtin

# Try to get domain password policy
getdompwinfo

# Try to enumerate different truste domains
dsr_enumtrustdom

# Get username for a defined user ?
getusername

# Query user, group etc informations
queryuser RID
querygroupmem519
queryaliasmem builtin 0x220

# Query info policy
lsaquery

# Convert SID to names
lookupsids SID
```
