# Git Config

Initial config

    git config --global user.name "myname"
    git config --global user.email "me@domain.com"

Create a new repository

    git clone ssh://git@github.net:/me/info.git
    cd ipc
    touch README.md
    git add README.md
    git commit -m "add README"
    git push -u origin master

Existing folder

    cd existing_folder
    git init
    git remote add origin ssh://git@github.net:/me/info.git
    git add .
    git commit -m "Initial commit"
    git push -u origin master

Existing Git repository

    cd existing_repo
    git remote rename origin old-origin
    git remote add origin ssh://git@github.net:/me/info.git
    git push -u origin --all
    git push -u origin --tags

Other

    git fetch --all
    git push origin writable:master
    git push --set-upstream origin writable
    git push origin <branchname>
    # New branch
    git checkout -b <branchname>
    # Switch branch
    git checkout <branchname>
    # List branch
    git branch
    # Add all changes
    git add -A
