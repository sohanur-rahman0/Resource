### Git CheatSheet
<img src="_Git cheat sheet dark (FINAL).png" alt="Git CheatSheet"/>

### Useful Git commands

#### Update a commit

```
git commit --amend -m "updated commit message"
```

#### If we want to keep the same commit message

```
git commit --amend -m --no-edit
```

#### Going back to older commit

```
git reset --hard <commitId> && git clean -f
```

#### Visualize git log

```
git log --graph --oneline --decorate
```

#### Create a new branch

```
git checkout -b <branchName>
```

#### Remove a file from commit

```
git rm <fileName> <fileName>
```
