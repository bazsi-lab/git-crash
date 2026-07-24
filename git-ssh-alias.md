╔══════════════════════════════════════════════════════════════╗
║        🔐 GIT + SSH CONFIG ALIAS — CHEAT SHEET             ║
╚══════════════════════════════════════════════════════════════╝


🟦 1. SSH CONFIG

~/.ssh/config

Host github-bash
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_bash
    IdentitiesOnly yes


Host github-ansible
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_ansible
    IdentitiesOnly yes



🟩 2. THE STRUCTURE TO REMEMBER

git@<SSH-CONFIG-ALIAS>:<GITHUB-OWNER>/<REPOSITORY>.git

        │                         │
        │                         └── selects the repository
        └── selects the SSH key



🟨 3. REAL EXAMPLES

git@github-bash:bazsi-lab/bash.git

git@github-ansible:bazsi-lab/ansible.git



🟪 4. CLONE A REPOSITORY

git clone git@github-bash:bazsi-lab/bash.git

git clone git@github-ansible:bazsi-lab/ansible.git



🟧 5. ADD REMOTE TO AN EXISTING LOCAL FOLDER

git init

git remote add origin \
git@github-bash:bazsi-lab/bash.git



🟥 6. FIX A WRONG EXISTING REMOTE

git remote set-url origin \
git@github-bash:bazsi-lab/bash.git



🟦 7. CHECK THE REMOTE

git remote -v

# Correct result:

origin  git@github-bash:bazsi-lab/bash.git (fetch)
origin  git@github-bash:bazsi-lab/bash.git (push)



🟩 8. TEST THE SSH ALIAS

ssh -T github-bash

ssh -T github-ansible



🟨 9. PUSH

git add .

git commit -m "Initial commit"

git branch -M main

git push -u origin main



❌ WRONG

git@github.com:bazsi-lab/bash.git

# "github.com" does not use the custom Host alias.
# SSH may select the wrong key.



✅ CORRECT

git@github-bash:bazsi-lab/bash.git

# "github-bash" matches:

Host github-bash



╔══════════════════════════════════════════════════════════════╗
║  LEFT SIDE  = SSH KEY                                       ║
║  RIGHT SIDE = GITHUB REPOSITORY                             ║
║                                                              ║
║  git@ALIAS:OWNER/REPOSITORY.git                             ║
╚══════════════════════════════════════════════════════════════╝
