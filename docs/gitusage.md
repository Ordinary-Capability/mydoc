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