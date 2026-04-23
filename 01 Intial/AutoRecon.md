

# 1- faster way with no dirbuster
## follow this way and do the dirsearch yourself using [[../02 Recon and Enumeration/02 Service scan/03- HTTP／s (80,443)]] template
## --exclude-tags=dirbuster 

### autorecon
```powershell
autorecon <% tp.frontmatter["RHOSTS"] %> --exclude-tags=dirbuster
```


### multiple targets
```powershell
autorecon -t targets.txt --exclude-tags=dirbuster -vvv
```


# 2- slow way, could take up to 9H for 3 targets
## autorecon
```powershell
autorecon <% tp.frontmatter["RHOSTS"] %> --dirbuster.threads=30 --dirbuster.tool=dirsearch --dirbuster.recursive
```

## multiple targets
```powershell
autorecon -t targets.txt --dirbuster.threads=30 --dirbuster.tool=dirsearch --dirbuster.recursive -vvv
```

