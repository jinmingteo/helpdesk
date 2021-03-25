# Directory
## [Git HelpDesk](#git-helper)

## [Linux HelpDesk](#linux-helper)

## [Docker HelpDesk](#docker-helper)

## [Python HelpDesk](#python-helper)

# Git Helper

## New to Github 

### Clone 
```
git clone https://github.com/jinmingteo/helpdesk.git
```

### Create new branch
```
git checkout -b new_branch_name
```

### Add edited files, commit and push
#### 1 file
```
git add edited_file.py
```

#### all files
```
git add .
```

#### Add only modified files
```
git add -u
```

### Commit
```
git commit -m "[title] commit msg"
```

### Push
#### master
```
git push origin master
```

#### sub-branch
```
git push origin new_branch_name
```

## Add submodule to existing repo
```
git submodule add git@github.com:jinmingteo/pytorch-image-models.git
```

## Remove submodule from existing repo

1. Delete the relevant section from the .gitmodules file.
2. ```git add .gitmodules```
3. ```git rm --cached pytorch-image-models ```
4. ```rm -rf .git/modules/pytorch-image-models ```

## New submodule in repo (Not cloned yet)
```git submodule update --init --recursive```

## Submodule update repos
```git submodule update --recursive --remote```

## Change submodule to https from ssh way
```git submodule sync```

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

## Add tags for Version Control
```
git tag -a v2.0 beb9829 -m "Deployment v2"
git push origin v2.0
```

# Linux Helper

## Sort file size

```
ls --sort=size -lh
```

## Find and **MOVE** txt

```
find . -name '*.txt' -exec mv '{}' /drive/images/ \;
```

## Kill python

```
pkill -9 python
```

## Kill previous job
```
kill %%
```

## Copy and Rename images in a directory
```
for i in *.jpg; do scp -p "$i" "../images/MOT17_11_`echo "$i" `"; done
```

## Compress video
```
 ffmpeg -i foo.avi -vcodec h264 -an foo.mp4
```

## Cut video
```
ffmpeg -i foo.mp4 -ss 00:00:00 -t 00:01:25 -async 1 foo_cut.mp4
```

## Crop video
```
ffmpeg -i in.mp4 -filter:v "crop=out_w:out_h:x:y" out.mp4

out_w is the width of the output rectangle
out_h is the height of the output rectangle
x and y specify the top left corner of the output rectangle
```

## Convert README.md to HTML
```
grip README.md --export readme.html
```
## Untangle Terminal and Apps
```
spotify & disown
pycharm-community . & disown
```

## Extract tar.gz or tar files (x for eXtract)
```
tar -xzvf archive.tar.gz
```

## Compress file to tar.gz or tar files (c for Compress)
```
tar -czvf archive.tar.gz /drive/persdet/ --exclude=/drive/persdet/junk --exclude=/drive/persdet/.cache
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

# Python Helper

## Check site packages
```
python -m site
```

## Create venv
```
virtualenv -p python3 venv/
source venv/bin/activate
```

## Hyphen package issues
```
## Assuming you have a ./pytorch-image-models/classification_model.py with a Classifier_Model object/class

import importlib
classification_py_file = importlib.import_module("pytorch-image-models.classification_model")
model = classification_py_file.Classifier_Model() #initialize the object in that file
```
