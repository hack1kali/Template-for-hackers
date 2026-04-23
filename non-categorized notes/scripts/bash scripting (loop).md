## 1- loop over numbers

```powershell
# this will loop over 1 ~ 65535 and output all the results to ports file.
for i in $(seq 1 65535);do echo $i; done > ports
```


## 2- loop over a text file and curl 

Here’s a clean **bash one-liner** way:

```bash
while read -r dir; do
    curl "http://example.com/$dir"
done < directories.txt
```

### Using `xargs` (faster, shorter):

```bash
xargs -I{} curl "http://example.com/{}" < directories.txt
```


## 3- [[Loop for LFI related test]]

* loop for LFI
```powershell
while read -r dir; do
    echo "[*] Checking $dir"
    curl -s "http://target.com/$dir" | grep -iE "pass|user|login|key|secret|admin|pwd"
done < directories.txt
```

- **Use xargs (faster alternative)**:
```powershell
cat directories.txt | xargs -I{} sh -c 'echo "[*] Checking {}"; curl -s "http://target.com/{}" | grep -i password'
```

