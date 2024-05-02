# Git


clone a specific branch
```shell
git clone --branch <branch_name> <repository_url>
```

### How to update existing Git repository

…or push an existing repository from the command line

```bash
git remote add origin <https://github.com/anticam/configs.git>
git branch -M main
git push -u origin main
```

### Git


| Task | Command | Description|
| --- | --- | --- |
| Initialize | `git init` | Initialize a new repository |
| Checkout | `git clone https://github.com/anticam/configs.git` | Clone a repository, a new folder configs created |
| Add a file | `git add main.cpp` | Add a single file (main.cpp) to the repository |
| Add all the files | `git add *`| Add all the files to the repository |
| Commit | `git commit -m "message"` | Commit to the HEAD. [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) |
| Push | `git push origin master` | Copy changes to remote repository |
| Connect | `git remote add origin <server>`| Connect to a remote repository |
| Branch | `git branch`| Show local branches |
| Branch | `git branch -r`| Show remote  branches |
| Branch | `git branch -a`| Show local and remote branches |
| Branch | `git checkout -b branch-name` | Create a new branch |
| Branch | `git  checkout branchname`| Switch to branch "branchname" |
| Branch master | `git checkout master` | Switch to master branch |
| Delete branch | `git branch -d branch-name` | Delete branch |
| Push branch | `git push origin branch` | Branch is available in remote repository |
| Pull | `git pull`| Update local repository from remote server. (fetch + merge) |
| Merge | `git merge branch` | Merge branch into active branch, includes all the Git commits in the history of target branch. |
| Diff | `git diff source target` | Compare changes between source and target branches |
| Log | `git log --author=user` | Logs |
| Log | `git log --author=user` ||
| Log | `git log --name-status` ||
| Log | `git log --patch` ||
| Log | `git log --pretty=oneline` ||
| Log | `git log --graph --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%an%C(reset)%C(bold yellow)%d%C(reset) %C(dim white)- %s%C(reset)' --all'` ||
| Replace | `git checkout -- filename`| Replace a local file |
| Drop | `git fetch origin` <br>  `git reset --hard origin/master` | Drop all the local changes |
| Show| `git show <commit> --stat`| Show what happened in a specific commit |
| Show | `git show <commit> -- <path to file>`| Show changes in a specific file |
| Squash | | [merge vs squash](https://betterprogramming.pub/why-i-prefer-regular-merge-commits-over-squash-commits-cadd22cff02c). Flattens all the Git commits to one commit in the target branch. |
| Trace | GIT_TRACE<br>`GIT_TRACE=1 git commit -m "message"` | for general traces|
| Trace | GIT_TRACE_PERFORMANCE | for logging the performance data |
| Trace | GIT_CURL_VERBOSE | for logging all curl messages, `curl -v` |

[Getting Started with Git and GitHub Part 1: Intro to Git and GitHub](https://dev.to/danielstai/getting-started-with-git-and-github-part-1-intro-to-git-and-github-k7a)  
[Git stash](<https://www.atlassian.com/git/tutorials/saving-changes/git-stash>)  
[Git Internals - Environment Variables](https://git-scm.com/book/en/v2/Git-Internals-Environment-Variables#Debugging)  

Git installation, usage [GeeksForGeeks](https://www.geeksforgeeks.org/working-on-git-bash/)  
Git commands [rogerdudler.github.io/git-guide/](https://rogerdudler.github.io/git-guide/)  
