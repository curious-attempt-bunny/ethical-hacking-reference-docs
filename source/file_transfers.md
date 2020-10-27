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

