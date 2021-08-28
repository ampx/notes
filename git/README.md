
```shell
#setup main development branch in central repo
git branch develop
git push -u origin develop

#clone git to dev machine
git clone https://github.com/ampx/Scheduler/
git checkout -b develop origin/develop

#create feature branch
git checkout -b new-feature develop

#ready to checkin
git status #check for new files
git add filename #stage new files
git commit #checkin all new changes

git pull origin develop #check if there are new changes up stream
git checkout develop
git merge new-feature
git push
#optional if want to remove new feature branch once checked into dev
git branch -d new-feature 

#start formal release
git checkout -b release-0.0.1 develop
#prepare release: build test, test logic, updted documentation, update pom version
git checkout master
git merge release-0.0.1
git push
git checkout develop
git merge release-0.0.1
git push
git branch -d release-0.0.1 #remove branch prep branch

#final tag and release
git checkout master
git -tag -a 0.0.1 -m "initial release" master
git push --tags

git checkout 0.0.1
#make build
mvn clean compile package
```
