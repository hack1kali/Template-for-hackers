```powershell
xfreerdp3 /cert:ignore /u:<% tp.frontmatter["domain-username"] %> /p:'<% tp.frontmatter["domain-password"] %>' /v:<% tp.frontmatter["RHOSTS"] %> +dynamic-resolution

```


standalone
```powershell
xfreerdp3 /cert:ignore /u:<% tp.frontmatter["domain-username"] %> /p:'<% tp.frontmatter["domain-password"] %>' /v:<% tp.frontmatter["RHOSTS"] %> +dynamic-resolution /cert:ignore
```


