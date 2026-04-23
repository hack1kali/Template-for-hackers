## For windows
# x64 - 64 bit
```powershell
x86_64-w64-mingw32-gcc adduser.c -o adduser.exe
```

# x86 - 32bit
```powershell
i686-w64-mingw32-gcc -o exploit.exe 40564.c -lws2_32
```
reference [Authby](6-%20Zettelkasten/Authby.md)


## for Linux
```powershell
gcc cve-2017-16995.c -o cve-2017-16995
```