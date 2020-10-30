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
@Searcher.filter = "samAccountType=805306368"
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

