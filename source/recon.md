# Recon

## recursive download

```
wget -r <url>
```

## DNS

```
host -l <domain> <nameserver>
```

## URL fuzzing

```
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u .../FUZZ -t 50 -oF logfile
```

```
wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt;archive.extentions.txt -u http://megahosting.htb/files/archive/FUZZ.FUZ2Z -t 50 --oF wfuzz.files.archive.txt --hc 404
```
## LFI

```
wget http://host/path?file=../index.php
```

Try [LFISuite](https://github.com/D35m0nd142/LFISuite).

## Mount NFS

```
sudo mount -o nfsvers=4 -t nfs remote.htb:/site_backups /mnt
```

## Public SMB

```
smbclient -L <host>
```

```
smbclient -L <host> -U 'a' -P ''
```

```
rpcclient -U FABRICORP\\tlavel 10.10.10.193
enumdomusers
enumprivs
enumprinters
```

## Detecting the SMB version

```
$ sudo tcpdump -A -vv -i eth0 host 192.168.0.82 | grep Samba
..
$ smbclient -L //192.168.0.38
..
..]........C.SMBs.......................d............Unix.Samba 2.2.1a.MYGROUP.
```

## SMB / Windows enum

```
enum4linux <host>
```

## Winrm

Brute forcing via msfconsole.
See also evil-winrm.
