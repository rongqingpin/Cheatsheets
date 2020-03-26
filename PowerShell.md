### PowerShell `.ps1` script syntax

```
function FuncName([string]$x, [int]$y, ...){
  return $z
}

# comments

if (){
  …
}

for ($i=i1; $i -lt i2; $i++){ # looping from i1 to i2-1
  …
  continue
}

$z = FuncName $x $y ...
```

**Data Types**  

`$array = value1, value2, ...`: fixed size  
`$array = New-Object System.Collections.Generic.List[type]`: not fixed size

**Operators**  

`!(…)`: not …  
`a -eq b`; `-ne`; `-lt`; `-le`; `-gt`; `-ge`  
`$string -like "…*..."`: pattern matching by regular expression, `*` is wildcard; `$str -match / -notmatch …`: substring search  
`$array -contains …`: return True / False

**Built-in Fuctions**

`$str.length -gt N`  
`$str2 = $str1.Replace("pattern1", "pattern2")`  
`$N = $array.Count`  
`$array.Add($value)`: must be expandable array

`$date = Get-Date -Format "yy-MM-dd"`   
`$dateOld = (Get-Date).AddMonths(-N)`: older by N months  
`$dateOld = Get-Date $dateOld -Format "yy-MM"`  

`Test-Path -Path $directory`: check if exist  
`Test-Path -Path $directory -NewerThan $date`  

`New-Item -Path $destination -Name $name -ItemType "directory"`: create directory  
`Copy-Item -Path $target -Destination $name`  
`Remove-Item -Path $content -options`: options can be `-Recurse` (remove all children in `$content`), `-WhatIf` (show what will happen w/o execution)  

`$object = Get-Item $fileName`  
`$objects = Get-ChildItem $directory <-Force> <-Recurse>`: get list of files in directory; `-Force` option includes hidden files  
`$content = $objects[$i].FullName`: get the name with path of the ith item (other properties include `Extension`, `CreationTime`, `LastWriteTime`)  

`Start-Process filepath\software.exe filepath\file_to_run -WindowStyle Hidden`: execute the program `file_to_run`  
`Start-Process filepath\software.exe '"file path\file to run"' -WindowStyle Hidden`: when the path / filename has blanks  

`Write-Host "text to display" -fore green`

**Objects, Events**  

`$fileWater = New-Object IO.FileSystemWatcher $folder, $filter -Property @{IncludeSubdirectories = $true;NotifyFilter = [IO.NotifyFilters]'FileName, LastWrite'}`: watching `$folder` & subdirectories  
`Register-ObjectEvent $fileWatcher Created -SourceIdentifier FileCreated -Action{...}`: take action if new file created  
`Unregister-event FileCreated`: terminate the file watcher (FileCreated defined as identifier is the above line)

---

### Windows command line

```bash
$ powershell # enters PS command line

$ Get-ExecutionPolicy -scope CurrentUser
$ Get-ExecutionPolicy -List

$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
$ Set-ExecutionPolicy -Scope CurrentUser

$ Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass # when the ps file is on network drive

$ filename.ps1 # run file
```

```bash
$ powershell.exe -noexit -WindowStyle hidden -file filename.ps1 # running in the background indefinitely
```
