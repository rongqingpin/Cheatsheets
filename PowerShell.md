### PowerShell `.ps1` script syntax

```
# comments

if (){
…
}

for ($i=i1; $i -lt i2; $i++){ # looping from i1 to i2-1
…
}
```

**Operators**

`!(…)`: not …  
`a -eq b`; `-ne`; `-lt`; `-le`; `-gt`; `-ge`  
`$string -like "…*..."`: pattern matching by regular expression, `*` is wildcard; `$str -match / -notmatch …`: substring search  
`$str.length -gt N`  
`$array -contains …`: `$array` defined as `…,…,…`

**Built-in Fuctions**

`$date = Get-Date -Format "yy-MM-dd"`   
`$dateOld = (Get-Date).AddMonths(-N)`: older by N months  
`$dateOld = Get-Date $dateOld -Format "yy-MM"`  

`Test-Path -Path $directory`: check if exist  
`Test-Path -Path $directory -NewerThan $date`  

`New-Item -Path $destination -Name $name -ItemType "directory"`: create directory  
`Copy-Item -Path $target -Destination $name`  
`Remove-Item -Path $content -options`: options can be `-Recurse` (remove all children in `$content`), `-WhatIf` (show what will happen w/o execution)  

`$objects = Get-ChildItem $directory`: get list of files in directory  
`$N = $objects.Count`  
`$content = $objects[$i].FullName`: get the name with path of the ith item  

`Start-Process filepath\software.exe filepath\file_to_run -WindowStyle Hidden`: execute the program `file_to_run`  
`Start-Process filepath\software.exe '"file path\file to run"' -WindowStyle Hidden`: when the path / filename has blanks  

---

### Windows command line

```bash
$ powershell # enters PS command line

$ Get-ExecutionPolicy -scope CurrentUser
$ Get-ExecutionPolicy -List

$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
$ Set-ExecutionPolicy -Scope CurrentUser

# Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass # when the ps file is on network drive

$ filename.ps1 # run file
```

```bash
$ powershell.exe -noexit -WindowStyle hidden -file filename.ps1 # running in the background indefinitely
```
