
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

git status                              # current state
git diff                                # unstaged differencies
git diff --staged                       # staged differencies
git add <file>                          # add one file to stage
git add .                               # add all everything to stage, recursirverly
git restore <file>                      # discard local unstaged changes, use carefully
git restore --staged                    # unstage, keep edits
git rm <file>                           # delete file + stage deletion
git mv old new                          # rename or move + stage
git commit --amend                      # edit last commit


# helpful history views

git log --oneline --decorate --graph -20        # list last 20 commit with details
git show <commit>                               #inspect commit
git blame <file>                                # who changed what lines

# sync / fetching 

git fetch                               # download remote updates
git fetch --all --prune                 # fetch all remotes, prune deleted branches
git pull                                # fetch + merge default, or fetch + rebase (if configured)

git show origin/main:path/to/file       # if the remote version of the file needed without switching

# branch management

git branch                              # list local branches
git branch -a                           # list local and remote branches
git branch -vv                          # show upstream tracking

# create branch from current heading

git switch -c feature-x                 # create and switch branch
git checkout -b feature-x               # old style

git switch main                         # switch branch
git checkout main                       # old style branch switch

# compare branches

git log --oneline --left-rigth --grap main.. feature-x
git diff main..feature-x                # what differs

# push branch + set upstream

git push -u origin feature-x

# delete branch local or remote

git branch -d feature-x                 # safe delete, only if merged
git branch -D feature-x                 # force delete local, be carefull
git push origin --delete feature-x      # delete remote branch

# rename branch

git branch -m oldname newname           # rename local
git push -u origin newname              # push new name
git push origin --delete oldname        # delete old remote name

# Merge feature into main (creates merge commit if needed)
git switch main
git pull
git merge feature-x
git push

# Rebase feature onto main (rewrites history; avoid in shared branches)
git switch feature-x
git fetch
git rebase main
git switch main
git merge feature-x                               # often fast-forward after rebase
git push

# conflict resolution

it status                                        # shows conflicted files
# open files, resolve markers <<<<<<< ======= >>>>>>>
git add <resolved-file>                           # mark resolved
git commit                                        # for merge
# or if you were cherry-picking:
git cherry-pick --continue
# or if you were rebasing:
git rebase --continue

# If you want to abort:
git merge --abort
git cherry-pick --abort
git rebase --abort

# cherry-pick

git cherry-pick <commit-hash>                     # apply one commit onto current branch
git cherry-pick <A>..<B>                          # apply a range (excluding A)
# If conflict:
git add <file>
git cherry-pick --continue
# Or abort:
git cherry-pick --abort

# tag versions milestones

git tag                         # list tags
git tag v1.0.0                  # lightweight tag
git tag -a v1.0.0               # annotated tag
git tag origin --tags           

# last-change recovery

git reflog                                        # find lost commits (local safety net)

# Undo last commit but keep changes staged/unstaged:
git reset --soft HEAD~1                           # keep staged
git reset --mixed HEAD~1                          # keep unstaged (default)

# Hard reset (DANGEROUS: discards local changes)
git reset --hard HEAD

# Reset local branch to match remote exactly (DANGEROUS)
git fetch
git reset --hard origin/main

# Remove untracked files/dirs (DANGEROUS)
git clean -nfd                                    # preview
git clean -fd                                     # execute

# diagnostic

git rev-parse --show-toplevel                     # repo root (are you in a repo?)
git status
git branch -vv
git remote -v
git log --oneline --decorate --graph --all -15











```
