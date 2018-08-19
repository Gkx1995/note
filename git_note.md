## git commands

##### 1. rebase

```bash
git log #check how many commit you want compress
git rebase -i HEAD~number #compress these commit and will pump into a commit vim window, pick the first one and s all the rest, store it and quit, dump into another window, delete all the commit and leave the the most important one and maybe add some new commit
git log #check if anything wrong
git status #check any new thing you want to add
git push --force #forcely push 
```

##### 2. stash and stash apply

```bash
git stash #put all current changes aside 
git checkout branch
git pull
git stash apply #apply local changes to the code that has been pulled to local
```

##### 3. deal with diverged branch

```bash
git remote update
git checkout branch
git reset --hard origin/branch
```

##### 4. reset to previous step

```bash
git log # operations till current HEAD
git reflog # operations of whole worktree
git reset --hard commit_id
```

