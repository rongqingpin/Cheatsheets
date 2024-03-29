## UNIX


### General

space is interpretted as command argument separator. e.g., `a = "a"` generates error

options of commands start with `-`; to use more than 1 options: `-xyz`

variable reference starts with `$`  
[environment & shell variables](http://www.ee.surrey.ac.uk/Teaching/Unix/unix8.html)  
`a=$(command)`: assign command result to variable `a`  
`declare -a array=("…" "…" …)`  
`((...))` denotes operator as arithmetic operation (e.g., +, -)

`<command1> | <command2>`: use output from 1 as input for 2  

```
if (($x == N)); then
  ...
else
  ...
fi
```

```
for i in "${array[@]}"
do
  ...
done
```

```
while [ $i -lt 10 ];
do
  ...
done
```

bash file start with `#! /bin/bash`

`# this is a comment`

`<command> --help`  
`man <option> <command>`: manual; option `-k word_to_look_for` shows functions that matches the pattern  
`whatis <command>`  
`apropos <keyword>`: show commands that contain keywords  
[macOS command line](https://ss64.com/osx/)  
`<cmd> + <shift> + <.>`: show / hide hidden files. [full list of methods listed here](https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/)  

### Files & directories

`~`: home directory  
`.`: current directory  
`..`: parent directory

`df -h`: summarize free disc space, in human-readable format  
`stat $f`: change \& open info for file  
`mkfs -t <type> <storage volume>`: type can be `ext2`, `ext3`, etc.  
`mount <volume> <directory>`

`cd <directory>`

`pwd`: print the whole path of the working directory

`ls <directory> <option>`: show files  
  * [option](https://ss64.com/bash/ls.html): e.g., `-hal` - `-a` all including hidden files, `-l` long format w/ file details, `-h` size info in human readable format

access rights: `r`, `w`, `x` (execute)  
`+`: add access; `-`: take away  
users: `u`, `g` (group), `o` (other than group or owner), `a` (all)  
`chmod <users><+ or -><rights> <filename>`: change rights; if specify multipy types of users, use `,` to separate  
`chmod <LMN> <filename>`: `L` for `u`, `M` for `g`, `N` for `o`; `0` as no permission, `1` for execute, `2` for write, `4` for read

`file *`: show the type of all files & directories

`mkdir <new_directory>`

`rm <file>`  
`rm -rf <directory>`: remove all contents without prompt  
`rmdir <directory>`

`cp X <X2>`: copy; if X2 = `.`, keep the same name to the current directory  
`scp X X2`: secure copy of remote files; X / X2 can be `<root>@<system>:/<directory>/<file>`

`mv X X2`: rename / move a file

`ln -s <target_directory> <link_name>`: create shortcut for target directory named link, e.g. `ln -s "$(pwd)" ~/link` creates link `link` in home directory for current directory


### Strings and File contents

`^` start of string; `$` end of string  
`*`: 0 or more characters  
`?`: 1 character  
`[a-z]`  
`'.. ..'`: if file name contains space, enclose by `''`

`y="...${x}..."`: concatenate string and variable value

`cat f`: show file content on screen  
* `cat > f`: from keyboard to file
* `cat f1 f2`: combine two files

`head <-N> f`: first N lines; if omitted, first 10  
`tail <-N> f`  
`less f`: one page at a time; press **space** to see next; type **q** to quit  
  * type **/<keyword>** to find and highlight
  * type **n** to find the next

`wc <option> f`: count
  * `-w`: word count
  * `-l`: line count
  	*  `wc -l file`: count no. of lines in file, outputting `n file`
   	*  `wc -l < file`: count no. of lines, outputting `n`

`grep <option> <'keywords'> f`: print the line containing keywords; default - case sensitive; option as
  * `-i`: ignore upper / lower case
  * `-v`: lines that do not match
  * `-n`: show line with line number
  * `-c`: count number of matches
  * `-A N`: showing N lines after the one with matched pattern
  * `-r`: recursively through all subdirectories
 example: `grep -ri "here goes some string" *` searches for the whole string in all folders


### Others

`clear`: clear the screen  
`!<pattern>`: recall previous command; pattern as `!` (last), `-N` (Nth most recent), `N` (Nth), or starting with `pattern`

`who`: show logged-on users

`<program> -V` or `<p> --version`: show the current version  
[tutorial on software compiling](http://www.ee.surrey.ac.uk/Teaching/Unix/unix7.html)

`sudo su`: superuser `su` / admin / root user  
`sudo <command>`: temporarily executes as `su`

`sh -c "..."`: calls program `sh` to execute command in `"..."`

`ps`: show running processes (with PID number)  
`pgrep -f 'filename'`: return PID of program 'filename'  
`jobs`: job list (with job number)  
reference jobs: `<command> <PID>` or `<command> %<job_number>`

`sleep nsecond`

---

default input: keyboard
* input from keyboard, type **Ctrl + d** to stop
* `< f`: input from file

`read x`: read user input as x; if input is number, can do number comparison directly

default output: screen (e.g., `echo`)
* `> f`: output to file; overwrite content
* `>> f`: append to file
 
`tee -a <filename>`: read inputs & attach to file. e.g., `echo "commands" | tee -a ...`
 
---
 
`<command> &`: run in the background (the program should not require user interaction)

for jobs in the foreground:
* type **Ctrl + c** to kill the process  
* type **Ctrl + z** to suspend
* `bg`: put a suspended foreground process to background

for jobs in the background / suspended:
* `fg %<job_number>`: restart & foreground; if number omitted, restart the last one
* `kill %<job_number>`; add option `-9` to kill process that refused

---

`find <location> <condition> <output>`:
* if location as `.`, search current directory & all sub-directories
* condition: `-name '<pattern>'`; `-size +<?M>`
  * condition modifier: `<condition1> -a <condition2>` AND; `-not <condition1>`
* output: `-print` show on screen; `-ls` list

`sort`: input from screen
* `sort < f1 > f2`

`diff f1 f2`: show the difference  

`rev f`: reverse each line in f

---

`latex <file.tex>`: will display 'Output written on file.dvi' if successful  
`bibtex <file.aux>`: if 'bibliography' is used for references; then repeat the `latex` command twice  
`xdvi <file.dvi> &`: view dvi file  
`dvipdf <file>`: convert to pdf  
`pdflatex file.tex`: convert to pdf  
`X`: force execute
