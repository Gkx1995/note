## git commands

##### 1. rebase

```bash
#check how many commit you want compress
git log

#compress these commit and will pump into a commit vim window, pick the first one and s all the rest, store it and quit, dump into another window, delete all the commit and leave the the most important one and maybe add some new commit
git rebase -i HEAD~number 

#check if anything wrong
git log

#check any new thing you want to add
git status

#forcely push 
git push -f
git push --force
```

##### 2. stash and stash apply

```bash
#put all current changes aside 
git stash

git checkout branch

git pull

#apply local changes to the code that has been pulled to local
git stash apply

```

##### 3. deal with diverged branch

```bash
git checkout branch
git reset --hard origin/branch
```

##### 4. reset to previous step

```bash
git log # operations till current HEAD
git reflog # operations of whole worktree
git reset --hard commit_id
```

