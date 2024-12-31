---
Title: CheatSheet
Date: 20.07.2023
Time: 17:47
Tags: [cheatsheet]
---

| *Description*             | *Origin Git command*    | *ZSH Alias* |
| ------------------------- | ----------------------- | ----------- |
| push DEV                  | git push origin dev     | gp dev      |
| push tags                 | git push origin --tags  | -           |
| push single tag           | git push origin v1.0.0  | -           |
| rebase into single commit | git rebase -i HEAD~2    |             |
| remove tag                | git tag -d \<tag name\> |             |
|                           |                         |             |

----------------
# GIT Re-base interactive

1. Re-base with interactive interface (squash last 2 commits)
   `git rebase -i HEAD~2`
2. Change the word "pick" to "squash" (or just "s" for short) for the commits you want to squash
   `pick abc123 Commit message 1
   `squash def456 Commit message 2`
3. Save and apply changes
4. Force push `ggf` or `git push --force origin $(current_branch)`

-------------------------------------

# GIT remove last commit
```bash
git reset --hard HEAD~1
```

-------------------------------------
# GIT fetch remote/single branch
> [!example]- featch remote branch
> ```bash
> git fetch origin feature-rt:feature-rt
> git checkout feature-rt
> ```

-------------------------------------
# GIT Squash / Re-base
### To make re-base from branch with remote/dev pulls
> [!example]- git merge --squash
> ```bash
> git checkout dev
> git pull origin dev
> git checkout -b 'RT-0000-squash'
> git merge --squash RT-0000-original
> git commit -m 'Commits squashed from RT-0000-original'
> git push origin RT-0000-squash
> git push origin --delete RT-0000-original
> ```

### git re-base interactive (all changes commited)
> [!example]- re-base interactive
> ```bash
> git checkout -b 'RT-0000-backup'
> git checkout RT-0000-original
> git rebase -i dev
> ```
 
```md
pick <hash1> First commit
squash <hash2> Merge commit from dev
squash <hash3> Second commit
```
complete re-base
```bash
git push origin RT-0000-original --force
```

-------------------------------------
# GIT Cherry & Cherry-pick

## Git cherry
show commit diff between branches
```bash
git checkout dev 
git cherry main
```

## Git cherry-pick
move commit from one branch into another
```bash
git checkout dev
git log feature-RT-0000 -1  (show last commit)
git cherry-pick <commit hash>
```
### Handling conflicts
If there are any conflicts during the cherry-pick, Git will stop and allow you to resolve them. After resolving the conflicts, you can continue the cherry-pick process with
```bash
git add <file_with_conflict>
git cherry-pick --continue
```
### Abort cherry-pick
```bash
git cherry-pick --abort
```

-------------------------------------

# GIT Log --pretty
### Simple pretty log
```bash
git log --pretty=oneline
```

### Medium pretty log
```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

### Detailed pretty log
```bash
git log --pretty=format:"%h %ad | %s%d [%an]" --date=short
```

### Graphical pretty log
```bash
git log --graph --pretty=format:"%h -%d %s (%cr) <%an>"
```

### Combined pretty log
```bash
git log --graph --all --pretty=format:"%h - %an, %ar : %s"
```

-------------------------------------
