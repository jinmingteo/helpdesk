# Directory
## [Git HelpDesk](#git-helper)

## [Linux HelpDesk](#linux-helper)

## [Docker HelpDesk](#docker-helper)

# Git Helper

## Add only modified files
```git add -u```

## Revert the file to its state in master
``` git checkout origin/master <filename> ```

## Uncommit

### not pushed yet
``` git reset HEAD-1 --soft``` 

### pushed to master
``` 
git checkout -b MyCommit (just in case)

git checkout master
git revert #hash of the commit you want to destroy
git push origin master
```

## remote repo
```
git remote -v
git remote set-url origin <forked_repo>
```

# Linux Helper

## Sort file size

```
ls --sort=size -lh
```

## find and **MOVE** txt

```
find . -name '*.txt' -exec mv '{}' /drive/images/ \;
```

# Docker Helper

## apt-get
```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
   make
```

## X / QT display

```
 xhost +local:docker && docker run --rm -e "DISPLAY=${DISPLAY}" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" <repo>
```
