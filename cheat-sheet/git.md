# Git

[Net Ninja - Git &GitHub Tutorial for Beginners](https://www.youtube.com/playlist?list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR)



## Git

### Workflows

#### Existing projects

##### Stages

**Modified** - Changes in code, modified, not committed
**Staging** - Add any changes files to staging that you want to commit
**Committed** - Any files in the staging area are added to the commit when me make one.

create file in project:
`touch <file>`

add one file to staging area:
`git add <file>`

or add every single modified file to the staging area:
`git add .`
`git status`

remove file from staging area:
`git rm --cached <file>`
`git status`

show logs
`git log`
`git log --oneline`


##### Undoing things

- Checkout commit - very safe (read only, no changes in code)
  
```shell
git log --oneline
a76412c UI5 showcase  
3b480f2 html5 repo  
9399ccc mount,umount  
```

  `git checkout a3b480f2`
- Revert commit - safe (undo, it looks like it never existed)
- Reset commit - unsafe (it could ruin the repository, permanently take you back in time to the specified commit)

##### Global settings

Set user name:
`git config --global user.name <name>`

Set email address:
`git config --global user.email <mail@domain>`


###### Download a repository content

Download configs folder:
`git clone https://github.com/anticam/configs.git`

or download to a specific, configuration folder
`git clone https://github.com/anticam/configs.git configuration`

or download a specific branch:
`git clone --branch <branch_name> <repository_url>`

###### Create a local repository and upload content

1. Create a repository on GitHub

2. Clone the repository:
`git clone https://github.com/anticam/configs.git`

###### When remote repository is not created:

1. Initialize local Git repo:
`git init`

2. Add files:
`git add .`

3. Create a repository on GitHub
4. Upload content:

```shell
git remote add origin <https://github.com/anticam/configs.git>
git branch -M main
git push -u origin main

// push all branches
git push --all origin
```


##### How to clone a specific branch
```shell
git clone --branch <branch_name> <repository_url>
```

##### How to connect local repository to existing Git repo:

…or push an existing repository from the command line

```bash
git remote add origin <https://github.com/anticam/configs.git>
git branch -M main
git push -u origin main

// push all branches
git push --all origin
```


##### Local repository initialization

`git init`

##### Adding files to repository

Add a single file to the repository:
`git add main.cpp`

Add all the files to the repository:
`git add *`
`git add .`


##### Commits

Commit to the HEAD:
`git commit -m "message"`
[Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) |


Show what happened in a specific commit:
`git show <commit> --stat`

Show chages in a specific file:
`git show <commit> -- <path to file>`

List commits in one line:
`git log --pretty=oneline`

[Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) |


##### Repository access

Clone a repository:
`git clone https://github.com/anticam/configs.git`
A new folder configs created |

Pull, update local repository from remote server ( fetch + merge ):
`git pull`

Push, copy changes to remote repository:
`git push origin master`

Connect to a remote repository:
`git remote add origin <server>`


##### Conflict handling

Merge branch into active branch:
`git merge branch`

It includes all the Git commits in the history of target branch.

Compare changes between source and target branch:

`git diff source target`

Replace a local file:
`git checkout -- filename`

Drop all the local changes:
`git fetch origin`
`git reset --hard origin/master`

Squash: 
[merge vs squash](https://betterprogramming.pub/why-i-prefer-regular-merge-commits-over-squash-commits-cadd22cff02c). Flattens all the Git commits to one commit in the target branch. |



##### Branches

List local branches:
`git branch`

List remote branches:
`git branch -r`

List local and remote branches:
`git branch -a`

Create a new branch:
`git checkout -b branch-name`

Switch to branch "branchname":
`git  checkout branchname`

Switch to master branch:
`git checkout master`

Delete a branch:
`git branch -d branch-name`

Push branch to remote repository:
`git push origin branch`

Push all the branches to origin:
`git push --all origin`


##### Tracing

General traces set GIT_TRACE environment variable:
`GIT_TRACE=1 git commit -m "message"`

Logging performance data:
`GIT_TRACE_PERFORMANCE`

Verbosity:
`GIT_CURL_VERBOSE`
for logging all curl messages, `curl -v`


###### Logging

Show logs per different filters:
`git log --author=user`
`git log --author=user`
`git log --name-status`
`git log --patch`
`git log --pretty=oneline`
`git log --graph --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%an%C(reset)%C(bold yellow)%d%C(reset) %C(dim white)- %s%C(reset)' --all'`




[Getting Started with Git and GitHub Part 1: Intro to Git and GitHub](https://dev.to/danielstai/getting-started-with-git-and-github-part-1-intro-to-git-and-github-k7a)  
[Git stash](<https://www.atlassian.com/git/tutorials/saving-changes/git-stash>)  
[Git Internals - Environment Variables](https://git-scm.com/book/en/v2/Git-Internals-Environment-Variables#Debugging)  

Git installation, usage [GeeksForGeeks](https://www.geeksforgeeks.org/working-on-git-bash/)  
Git commands [rogerdudler.github.io/git-guide/](https://rogerdudler.github.io/git-guide/)  
