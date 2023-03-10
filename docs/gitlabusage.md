# Gitlab Usage
##  Data Backup and Restore
- Backup datas and config files which contains the key for encrypted info in datas
```
sudo gitlab-backup create  #12.2 or later
gitlab-rake gitlab:backup:create #12.1 or earlier
/etc/gitlab/gitlab-secrets.json
/etc/gitlab/gitlab.rb
```
Store the *backup.tar* file in */var/opt/gitlab/backups*
- Restore  
Copy *backup.tar* file back to */var/opt/gitlab/backups*
Stop some service *gitlab-ctl stop sidekiq*
Back up the data with commands below
```
sudo gitlab-backup restore BACKUP=11493107454_2018_04_25_10.6.4-ce #12.2 or later
gitlab-rake gitlab:backup:restore BACKUP=11493107454_2018_04_25_10.6.4-ce #12.1 or earlier
```
Replace config files with the old ones
Reconfigure and restart gitlab service
```
sudo gitlab-ctl reconfigure
sudo gitlab-ctl restart
sudo gitlab-rake gitlab:check SANITIZE=true
```
[Known issue](https://gitlab.com/gitlab-org/gitlab-foss/-/issues/62759/?_gl=1*novgys*_ga*MTg5NTc2OTUwNy4xNjc1MDcwNzkw*_ga_ENFH3X7M5Y*MTY3NTgzNzcyNy4xNy4xLjE2NzU4Mzk3NjEuMC4wLjA.)  
To fix: *sudo chown -R registry:registry /var/opt/gitlab/gitlab-rails/shared/registry*

## Gitlab-runner Usage
- Sign in as *gitlab-runner* user
```
sudo su - gitlab-runner
```

## Gitlab-CI/CD
- .gitlab-ci.yml template
```
before_script:
  - git config --list
  - export COMMIT_TIME=$(date '+%Y-%m-%d')

variables:
  GIT_STRATEGY: clone

stages:
  - build:a
  - build:b
  - test
  - release
  - deploy

job_build_a:
  stage: build:a
  only:
  script:
    - echo "Build job a start ..."
#  artifacts:
#    expire_in: 7 days
#    paths:
#      - aosp/out/target/product/fy12b/*.img
#    name: aosp-fy12b-$COMMIT_TIME

job_build_b:
  stage: build:b
  only:
  script:
    - echo "Build job b start ..."

job_test:
  stage: test
  script:
    - echo "test job."
    
job_release:
  stage: release
  script:
    - echo "Job release ..."
    
job_deploy:
  stage: deploy
  script:
    - echo "Job deploy ..."
```

## Reference
https://docs.gitlab.com/ee/raketasks/backup_gitlab.html


