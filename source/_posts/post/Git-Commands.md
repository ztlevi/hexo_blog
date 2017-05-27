---
title: Git Commands
date: 2017-05-25 20:04:43
categories:
tags: git
---

Git Commands
============

Create a new repository on the command line
-------------------------------------------

-   git init
-   git add README.md
-   git commit -m "first commit"
-   git remote add origin <https://github.com/ztlevi/DeployWebsite.git>
-   git push -u origin master
-   Push an existing repository from the command line
-   git remote add origin <https://github.com/ztlevi/DeployWebsite.git>
-   git push -u origin master

<!--more-->

1. Creating repository
----------------------

| git commands             | Description                       |
|--------------------------|-----------------------------------|
| git init                 | Initialize a git project          |
| git add <filename>       | . or * means all new files       |
| git rm —cached -         | Remove all files from cache       |
| git commit               | Commit your changes to repository |
| git commit -a            | Combined the add and commit step  |
| git status               | Check what the file changed       |
| git diff readme.md       | See the changes of readme.md      |
| git diff v2.5 HEAD       | Compare the current HEAD to v2.5  |

The commit you are currently on is known as the HEAD commit.

2. Version rollback
-------------------

| git commands                    | Description                                                                          |
|---------------------------------|--------------------------------------------------------------------------------------|
| git log                         | Show the logs(SHA)                                                                   |
| git log --pretty=oneline        | Show the logs concisely                                                              |
| git reflog                      | Get the version number(first 7 characters of the SHA)                                |
| git reset --hard HEAD^          | Go back to the last version, --hard is used to reset the index and working directory |
| git reset --hard HEAD@{n}       | Go back to the nth versions before                                                   |
| git reset --hard version_number | Reset to the specific version                                                        |

3. Undo changes and delete files
--------------------------------

| git commands                       | Description                                            |
|------------------------------------|--------------------------------------------------------|
| git checkout HEAD <filename>    | Undo the file changes and recover the file to the HEAD |

<img src="https://ww1.sinaimg.cn/large/006tNc79gy1fd8dh32mgwj31960q041o.jpg" alt="img" title="image title"/>
3.1 Delete commits
------------------

| git commands                      | Description                                                                       |
|-----------------------------------|-----------------------------------------------------------------------------------|
| Git glog                          | See commit ids                                                                    |
| Git rebase -i commit<sub>id</sub> | Edit the commits from HEAD to commit<sub>id</sub> (delete line to remove commits) |
| Git push -f origin branch         | Force push to origin branch                                                       |

4. Remote repository
--------------------

### Step 1: Create SSH Key

ssh-keygen -t rsa -C "your email" ---> generate puclic/private rsa key pair

### Step 2: Open github -> settings -> SSH and New GPG keys -> New SSH keys

Fill anything in the title and copy the id_rsa.pub to the key text box. Then click Add Key.

### a. Add remote repository

| git commands                                                                                 | Description                                                                     |
|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| git remote add origin <https://github.com/ztlevi/MRS.git>                                    | Add remote repository                                                           |
| git remote add origin git@github.com:ztlevi/MRS.git                                          | The same.                                                                       |
| git push -u origin/dev dev <br>= git push -u origin dev<br>= git push origin dev      | Set upstream for git pull/status. dev branch will be created if not existed.    |
| git checkout origin/dev –b dev                                                               | Checkout to dev branch and set upstream to origin/dev. Contain the next command |
| git branch -u origin/dev dev <br>= git branch -u origin dev                        | dev set up to track remote branch dev from origin.                              |

After that, use git push/git push origin master

### b. Clone the remote repository

`git clone remote_location  //clone_directory`

Remote location can be local or online location, such as http/ssh. If there is no clone_directory, then the default directory is the root directory.

5. Create and merge branch
--------------------------

| git commands                           | Description                                                                                                                     |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| git checkout -b <name>           | Create and switch to the branch created. This command equals<br> the following two commonds git branch dev and git checkout dev |
| git branch (-v)                        | List all the branches                                                                                                           |
| git branch <name>                | Create branch                                                                                                                   |
| git checkout <name>              | Switch branch and will automaticlly merge                                                                                       |
| git branch -d <name>             | Delete branch                                                                                                                   |
| git push origin -d <branch name> | DeleteDelet remote branch                                                                                                            |

On master branch

| git commands                   | Description                                |
|--------------------------------|--------------------------------------------|
| git merge dev                  | Merge dev into the master                  |
| git merge --no-ff -m "..." dev | Merge without fast forward mode            |
| git merge origin/master        | Merge into the remote origin/master branch |

6. Bug branch
-------------

| git commands    | Description                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------|
| git stash       | record the current state of the working directory and the index, <br>and go back to the clean HEAD. |
| git stash list  | show the working directory                                                                      |
| git stash apply | recover the working directory                                                                   |
| git stash drop  | delete the WIP(working in process)                                                              |
| git stash pop   | equals apply + drop                                                                             |

7. Cooperation
--------------

| git commands                              | Description                        |
|-------------------------------------------|------------------------------------|
| git remote                                | check the remote repository status |
| git remote -v                             | check the detailed information     |
| git remote remove <name>            | Remove the remote                  |
| git remote rename <old> <new> | Rename the remote                  |
