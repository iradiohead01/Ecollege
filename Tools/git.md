# Git Knowledge
- [Git Knowledge](#git-knowledge)
    - [git merge command](#git-merge-command)
    - [remove remote branch](#remove-remote-branch)
    - [little tips](#little-tips)

## git merge command

- git reset <commit id last fetched from master>

    roll back to last merge version of master branch

- git stash

    save our own change recently

- git fetch origin
  
    update HEAD version to the newest master version

- git merge origin/master

    merge code

- git stash pop

    pop out over own code and merge, if have conflict, resolve them manually

- git add .

    add all your own changed code

    git commit -m "commit message"

- git push origin branch_name -f

    push your commit to remote repository forcedly

## remove remote branch

- remove local branch

git branch -D branch_name

- remove remote branch

git push origin --delete branch_name

## little tips

- how many lines modified

git log -r c73792a4303417c001470df1df49a4031f2a4a66 --numstat