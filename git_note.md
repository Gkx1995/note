## git commands

##### 1. rebase

```bash
git log #check how many commit you want compress
git rebase -i HEAD~number #compress these commit and will pump into a commit vim window, pick the first one and s all the rest, store it and quit, dump into another window, delete all the commit and leave the the most important one and maybe add some new commit
git log #check if anything wrong
git status #check any new thing you want to add
git push --force #forcely push 

##############
#commit deleting
git rebase --onto <branch>~2 <branch>~1 branch
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

git push --force origin branch
```

##### 4. reset to previous step

```bash
git log # operations till current HEAD
git reflog # operations of whole worktree
git reset --hard commit_id
```

##### 5. `git pull` pulls remote and merge to work dir, while `git fetch` fetches remote to local commit repo and does not merge to work dir

##### 6. `git clean` cleans all the untracked files as well as untracked directory

##### 7. `backporting` 

```bash
git checkout version-branch #Branch 'v20190226' set up to track remote branch 'v20190226' from 'origin'.
arc feature new-branch-off-version-branch # same as git checkout -b new-branch-off-version-branch
arc patch --nobranch feature-branch # function as git cherry-pick feature-branch, fetch feature-branch commits to version-branch, might have some conflict, just fix it, git add it, and git cherry-pick --continue
arc diff --create # pull request to merge to version-branch
```

##### 8. Rebase on release branch

```bash
git checkout relase-branch
git pull
git checkout the-branch-off-release-branch
git pull --rebase #never run sp-rebase on release branch!!
arc diff
```

#####9. `git stash apply "stash@{2}"`