

# python3 
1- create virtual enviroment
```powershell
python3 -m venv venv
```
2- activate it 
```powershell
source venv/bin/activate
```
3- install the needed package 
```powershell
pip install git-dumper
```

4- run it against your target
```powershell
git-dumper http://<% tp.frontmatter["VHOST"] %>/.git .
```

5- git log 
```powershell
# Log information of the current repository.
git log
```

6- git show log
```powershell
# This will display the log of the stuff happened, like commit history which is very useful
git show 80ad5fe45438bb1b9cc5932f56af2e9be7e96046
```



reference:
[[6- Zettelkasten/Github recon Example from OSCP-A machines]]
