### Useful Git commands

#### Update a commit

```
git commit --amend -m "updated commit message"
```

#### If we want to keep the same commit message

```
git commit --amend -m --no-edit
```

#### Remove the last commit from remote repository

```
git revert HEAD [main 2218b9e]
```
