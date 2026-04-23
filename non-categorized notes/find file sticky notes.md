# Search in names (files & folders)
```powershell
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue |
    Where-Object { $_.Name -match 'StickyNote|Sticky Notes' } |
    Select-Object -ExpandProperty FullName
```
