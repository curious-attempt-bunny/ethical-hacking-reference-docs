# File Transfers

## Windows

### Non-interactive FTP

```
echo open ipaddress> ftp.txt
echo USER username>> ftp.txt
echo password>> ftp.txt
echo bin>> ftp.txt
echo GET filename>> ftp.txt
echo bye>> ftp.txt
ftp -n -v -s:ftp.txt
```

### VBScript wget

```
curl -L -O https://gist.githubusercontent.com/maddouri/da64f298e19bff0cd1ce46ee83317bfe/raw/90080a73b892b09dde9dd2c787814bac502d7f46/wget.vbs
```
```
cat wget.vbs | sed -e 's/^/echo /' | sed -e 's/$/>> wget.vbs/' | xclip -i -selection clipboard
```
```
cscript wget.vbs <url> (file)
```
