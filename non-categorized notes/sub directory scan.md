
```powershell
gobuster dir -u http://<% tp.frontmatter["RHOSTS"] %> -w /usr/share/wordlists/dirb/common.txt -s "200,301" -x "htm,html,php,cgi" -b ""
gobuster dir -u http://<% tp.frontmatter["RHOSTS"] %> -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -s "200,301" -x "htm,html,php,cgi" -b ""



dirsearch -u http://<% tp.frontmatter["RHOSTS"] %> -w /usr/share/wordlists/dirb/common.txt --exclude-status 401,302,500
dirsearch -u http://<% tp.frontmatter["RHOSTS"] %> -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt --exclude-status 401,302,500

   Response Codes to Focus On: 
     - 200 OK → The requested resource exists and is accessible. 
     - 301 Moved Permanently → Can indicate alternative resource locations. 
     - 403 Forbidden → The resource exists but is restricted. 
     - 404 Not Found → The resource does not exist, but may reveal hidden directories. 

   Response Codes to Avoid: 
     - 302 Found → Temporary redirection. 
     - 401 Unauthorized → Indicates authentication is required. 
     - 500 Internal Server Error → Might indicate misconfiguration but not always useful. 
```
