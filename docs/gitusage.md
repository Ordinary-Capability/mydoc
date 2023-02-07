# Common Git Usage notes

- cherry-pick with no auto commit
```
git cherry-pick -n <hash>

git commit -m <comment>
```

- append current commit into previous one with no message edit(use the old commit message)
```
git commit --amend --no-edit
```

