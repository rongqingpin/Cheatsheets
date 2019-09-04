## Git / GitHub

`$ git status`  
`$ git log`  
`$ git diff HEAD`: show the difference with the most recent commit  
`$ git remote -v`: check which remote directory is connected

---

### creating a new repository

- create a repository online

- **if copying from online**

    2. `$ git clone <url_of_online_repository> <-branch remote_branch_name>`: default remote branch is master, can be omitted

- **if files existing locally**

    1. go inside the folder to be uploaded
    2. `$ git init`
    4. `$ git add <...>`
    5. `$ git commit -m “<explanatory texts about this change>”`
    6. `$ git remote add <remote_name> <url_of_online_repository>`
        * if copied from another online repositories, may need to reset url (see `make changes / rename a repository`)
    7. `$ git push -u <remote_name> <master>` (`-u`: git remembers the name and branch; next time can be omitted. Pushed to master branch on remote)

- generate README file (locally)
    1. `$ echo “# <repository name>” >> README.md`

- create .gitignore file (locally)
    1. go to the folder which contains .git folder
    2. `$ touch .gitignore`
    3. `$ open .gitignore`
    4. add the files / directories to be ignored (`directory_in_home_folder/sub_directory/.../`)

---

### make changes

- from remote to local
    1. `$ git pull <remote_name> master`: should be at a local commit that is present in remote; pull combines fetch and merge
    2. may need to:
        1. `$ i`
        2. write the merge message
        3. press **esc**
        4. `$ :wq`
        5. press **enter**
        
- from local to remote
    1. `$ git add <...>`
        * to undo: `$ git checkout -- <...>`
    2. `$ git commit -m <'...'>`
        * to unstage files: `$ git reset <...>`
    3. `$ git push`: to master branch origin
        * if want to update to a different branch: `$ git push <remote_name> <local_branch>:<remote_branch>`

- rename a repository
    1. rename online
    2. local: `$ git remote set-url <name> <new url>`

- remove changes
    * `$ git reset <location>`: move back
    * `$ git revert HEAD`: new commit that reverses the most recent commit

- select certain commits as new commits
    * `$ git cherry-pick x y ...`: copy commits (can be from any OTHER branch) and paste in HEAD
    * `$ git rebase x <y>`:
      1. select the commits that are different between the two; if y omitted, y = HEAD
      2. copy & attach the different commits to x
      3. HEAD moved to the end of new commits
    * `$ git rebase -i <location>`: a UI shows up which enables select & reorder commits; new branch with selected commits starting from location

#### git add

* `$ git add <file / directory>`
* `$ git add '*.<filetype>'`
* `$ git add -A` ALL
* `$ git add .` new & modified; without deleted files
* `$ git add -u` modified & deleted; without new files

---

### branches

* `$ git branch`: show the local branches
* `$ git branch <branch_name>`: create new branch
* `$ git branch <branch_name> <location>`: define a past commit

* move commit (HEAD) or branch:
    * `$ git branch -f <branch> <location>`
    * `$ git checkout <location>`: go to the branch / move HEAD (if location is not branch name, HEAD is detached)
        * `$ git checkout -b <branch>`: create and checkout
    * location can be branch name / HEAD / hash (see git log)
        * add `^N` right after to move 1 level up; N specifies which branch to go (1 directly up)
        * add `~N` to move N levels up
        * these two can combined for multiple times; if N omitted, N = 1

* `$ git branch -d <branch>`: delete

* `$ git gui browser <branch>`: view all the files and directories

* `$ git merge <branch>`: currently in master, merge with branch
    - if have conflict, first use `$ git status` to inspect which file has issue; then re-open the file-in-question through editor and resolve the conflict; finally `git add .` and `git commit ...` and the branch will be merged

* by default, master tracks origin (master in remote); to change this: `$ git branch -u <origin> <branch>`

---

### tags

`$ git tag <tag> <location>`: tag cannot be moved / changed  
`$ git tag -a <tag> -m "description"`

`$ git show <tag>`

`$ git describe <location>`: compare location with its closest ancestor tag
