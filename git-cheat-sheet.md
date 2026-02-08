
author:         saba
version:        v1.0
date:           Februar 2nd, 2026


# Git Cheat Sheet

## Git Config Levels

### --system - System Levels

- applies all users on the system
- stored system wide configuration file `/etc/gitconfig`
- requires administrative privileges

`git config --system core.editor "vim"`

### --global - Global Levels

- applies to your user account accross all repositories on the actual computer
- stored in our home directory, usually in `~/.gitconfig`

`git config --global user.name "name" `

### Local Level (no flag)

- applies on the specific directory
- stored in `.git/config` inside the repository
- overrides global and system settings

` git config user.name "repo-specific-name"

### Summary

Level 	Command example 	Scope
System 	git config --system 	All users on the machine
Global 	git config --global 	Your user account (all repos)
Local 	git config (no flag) 	Specific repository


```bash
# global config

git config --global init.defaultBranch main                     # set the branch for new repos on "main"
git config --global pull.rebase false                           # keep merges by default (simple)
git config --global fetch.prune true                            # remove deleted remote branches locally
git config --global core.editor "vim"                           # optional: set desired editor
git config --global color.ui auto                               # colored output on terminal, if supported

git config --global merge.tool meld                             # set default merge tool
git config --global push.default simple                         # set default push behavior

git config --global alias.co commit                             # set "git co" as alias to "git commit" command


git config --global user.name "name"                            # set the default user name -global 
git config --global user.email "email"                          # set the default user eimal addr -global


# starting a new repo: first make an online empty repo - first local push

mkdir myrepo && cd myrepo
git init                                                # init the folder to git repo
git branch -M main                                      # ensure branch name is main
git remote add origin git@github.com:myname/myrepo.git  # set the remote repo url
git remote -v                                           # display the remote repositories that are associated with the local git repo

git status      
git add .                           # add all files to stage
git commit -m "Initial commit"      # first commit
git push -u origin main             # specify which remote (origin) and which branch (main) to push to.
git push                            # the rest of the time, if nothing is changes


# clone an existing repo, joining the project/repo

cd /path/toProject
git clone git@github.com:user/repo.git

cd repo

git status
git remote -v
git branch -a
git log --oneline --decorate -10     # show commit history, each record in one line, show references (branch names) for each, with output limit


# normal daily workflow

git status              # show status
git pull                # get the latest
        # edit files
git status
git add .
git commit -m "describe changes"
git push

git add -p              # stating interactively parts of the changes

# remote management

git remote -v                                           # list of remotes
git remote show origin                                  # show detailed remote info
git remote rename origin github                         # rename remote alias
git remote set-url origin git@github.com:user/repo.git  # set remote repo url        
git remove origin                                       # remove remote alias completely

# file / change management










```
