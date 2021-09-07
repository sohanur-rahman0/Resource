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
