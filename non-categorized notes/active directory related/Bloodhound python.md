
###### Bloodhound python
```powershell
bloodhound-python -u <% tp.frontmatter["domain-username"] %> -p <% tp.frontmatter["domain-password"] %> -ns <% tp.frontmatter["RHOSTS"] %>  -d <% tp.frontmatter["VHOST"] %>  -c all
```