# Common Git Usage notes

- cherry-pick with no auto commit
```
git cherry-pick -n <hash> #single commit
git cherry-pick -n <hash>..<hash> #a range of commits
git commit -m <comment>
```

- append current commit into previous one with no message edit(use the old commit message)
```
git commit --amend --no-edit
```

- Merge with no auto commit
```
git merge <target_branch> --no-commit --no-ff
git restore --staged <file>  #undo some added file
git merge --continue  #continue merge
```

- Remove untracked files
```
git clean -n #dry run
git clean -fd #f for force, d for directory
```

- Reset From Remote Branch
```
git fetch origin
git reset --hard origin/master
```

- git submodule   
A repoA can be linked to a subdirectory in repoB
```
git submodule add -b master https://gitlab.fullhan.com/zhous463/AudioTool.git aqtools_pc
commit -m "add aqtools_pc submodule"
```
User use additional commands below to pull submodule directory content
```
git submodule update --init --recursive
git submodule update --recursive --remote
```
*Note*: Authentication is need for gitlab-runner run CI jobs to pull the submodule content, it can be a bit more complicated than run a normal repo CI job.
