# Example Foothold -> User -> Root

## Mine

### Footholds

* auth brute forcing using `cewl` wordlist
* LFI for tomcat user creds
* fuzzing urls for credentials file
* writable NFS for ssh key
* readable SMB with cred reuse in source code

### User

* password in plain text in Apache James mailbox
* reverse shell via ms sql powershell exec (msfvenom base64 encoded payload)
* admin UI connects to my mysql instance, load into table php file with reused credentials
* upload reverse shell war to Tomcat (msfvenom payload)
* `su -` to bypass `rbash` limitations on `export PATH`
* file upload exploit for reverse shell (searchsploit)

### Root

* lxd group allows to run instance mounting root
* sudo bug allows `(ALL, !root)` as root using `sudo -u#-1`
* override PYTHONPATH and `sudo` execute python script
* kernel exploits

## Other people's

### Foothold

* password to printer via winrm
* credentials in readable file share
* fuzz URLs for documents (wordlist + extensions)
* single quote in form field hints at sql injection vuln
* hints of additional virtual hosts to access more content

### User

* evil-winrm with creds for shell 
* upload reverse shell php
* overwrite writable script file executable via sudo as root

### Root

* windows priv SeLoadDriverPrivilege -> ExploitCapcom
* find a hash of root password and crack it using `john`


