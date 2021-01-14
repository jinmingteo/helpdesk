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

## Fetch a remote PR into your local repo
```
git fetch origin pull/ID/head:BRANCHNAME
git checkout BRANCHNAME
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

## Compress video
```
 ffmpeg -i foo.avi -vcodec h264 -an foo.mp4
```

# Docker Helper

## apt-get
```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
   make
```

## X / QT display issue

```
 xhost +local:docker && docker run --rm -e "DISPLAY=${DISPLAY}" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" <repo>
```

## No 'rights' to docker images / Permission Issues

- Dockerfile to receive arguments, and creates a new user called “user” (put at end of Dockerfile)
```
ARG USER_ID
ARG GROUP_ID

RUN addgroup --gid $GROUP_ID user
RUN adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID user
USER user
```

- Build with args
```
docker build -t myimage \
  --build-arg USER_ID=$(id -u) \
  --build-arg GROUP_ID=$(id -g) .
```

- Run Docker w explicit user id and group id
```bash
 docker run -it \
  --user "$(id -u):$(id -g)" \
```



