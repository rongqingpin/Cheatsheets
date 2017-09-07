### UNIX

`~`: home directory  
`.`: current directory  
`..`: parent directory

`$ clear`: clear the screen  
`!<pattern>`: recall previous command; pattern as `!` (last), `-N` (Nth most recent), `N` (Nth), or starting with `pattern`

options of commands start with `-`; to use more than 1 options: `-xyz`

`*`: 0 or more characters  
`?`: 1 character

variables start with `$`  
[environment & shell variables](http://www.ee.surrey.ac.uk/Teaching/Unix/unix8.html)

default input: keyboard
* input from keyboard, type **Ctrl + d** to stop
* `< f`: input from file

default output: screen
* `> f`: output to file; overwrite content
* `>> f`: append to file

`$ <command1> | <command2>`: use output from 1 as input for 2  

`$ who`: show logged-on users

`$ <program> -V` or `<p> --version`: show the current version  
[tutorial on software compiling](http://www.ee.surrey.ac.uk/Teaching/Unix/unix7.html)

`$ man <command>`: manual  
`$ whatis <command>`  
`$ apropos <keyword>`: show commands that contain keywords  
[macOS command line](https://ss64.com/osx/)

---

`$ ps`: show running processes (with PID number)  
`$ jobs`: job list (with job number)
reference jobs: `<command> <PID>` or `<command> %<job_number>`

`$ <command> &`: run in the background (the program should not require user interaction)

for jobs in the foreground:
* type **Ctrl + c** to kill the process  
* type **Ctrl + z** to suspend
* `$ bg`: put a suspended foreground process to background

for jobs in the background / suspended:
* `$ fg %<job_number>`: restart & foreground; if number omitted, restart the last one
* `$ kill %<job_number>`; add option `-9` to kill process that refused

---

`$ cd <directory>`

`$ pwd`: print the whole path of the working directory

`$ ls <directory> <option>`: show files  
  * option: `-a`: all including hidden
  * `-l`: show details about files

access rights: `r`, `w`, `x` (execute)  
`+`: add access; `-`: take away  
users: `u`, `g` (group), `o` (other than group or owner), `a` (all)  
`$ chmod <users><+ or -><rights> f`: change rights

`$ file *`: show the type of all files & directories

`$ find <location> <condition> <output>`:
* if location as `.`, search current directory & all sub-directories
* condition: `-name '<pattern>'`; `-size +<?M>`
* output: `-print` show on screen; `-ls` list

---

`$ mkdir <new_directory>`

`$ rm <file>`  
`$ rmdir <directory>`

`$ cp X <X2>`: copy; if X2 = `.`, keep the same name to the current directory

`mv X X2`: rename / move a file

---

`$ cat f`: show file content on screen  
* `$ cat > f`: from keyboard to file
* `$ cat f1 f2`: combine two files

`$ head <-N> f`: first N lines; if omitted, first 10  
`$ tail <-N> f`  
`$ less f`: one page at a time; press **space** to see next; type **q** to quit  
  * type **/<keyword>** to find and highlight
  * type **n** to find the next

`$ grep <option> <'keywords'> f`: default - case sensitive; option as
  * `-i`: ignore upper / lower case
  * `-v`: lines that do not match
  * `-n`: show line with line number
  * `-c`: count number of matches

`$ wc <option> f`: count
  * `-w`: word count
  * `-l`: line count

`$ sort`: input from screen
* `$ sort < f1 > f2`

`$ diff f1 f2`: show the difference
