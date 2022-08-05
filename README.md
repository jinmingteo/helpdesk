# Directory
## [Git HelpDesk](#git-helper)

## [Linux HelpDesk](#linux-helper)

## [Docker HelpDesk](#docker-helper)

## [Python HelpDesk](#python-helper)

## [JupyterNotebook HelpDesk](#jupyter-helper)

## [Pytorch HelpDesk](#pytorch-helper)

## [tmux HelpDesk](#tmux-helper)

# Git Helper

## New to Github 

### Set up global .gitignore
```
Get .gitignore from this repo (covers Python, Pycharm & VSCode)
git config --global core.excludesfile '~/.gitignore'
```

### Clone 
```
git clone https://github.com/jinmingteo/helpdesk.git
```

### Clone branch
```
git clone -b main_repo https://github.com/jinmingteo/pytorch-image-models.git
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

#### Remove added files
```
git reset HEAD edited_file.py
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

## Force submodule to be updated whenever main repo git pull
```
git config --global submodule.recurse true
```

## git config for local
```
# check global and local list
git config --list 
# amend local 
git config user.email jinmingteo95@gmail.com 
# amend global
git config --global user.email jinmingteo95@gmail.com
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
``` git reset --soft HEAD~1``` 

### check local commits
``` git diff origin/master..HEAD ```

### pushed to master
``` 
git checkout -b MyCommit (just in case)

git checkout master
git revert #hash of the commit you want to destroy
git push origin master
```

### edit pushed commits (not recommended if proj has other collaborators)
```
git reset --soft HEAD~1 (reset to prev commit)
git stash (stash prev commit code)
git push -f origin master (push to ensure master is in prev commit)
git stash pop (get prev commit code)
git add (add other changes)
git commit 
git push origin master
```

### revert without traces
```
git reset --hard HEAD~x will remove the last x commits from the current commit that the HEAD is at (basically the current status of your local repo)
git push -f origin master
```

## Forked / Remote repo
```
git remote -v
git remote set-url origin <forked_repo>
```

### Add multiple remote repos (suitable for HDD transfer)
```
git remote add a urla
git remote add b urlb
```

### Update all remote repos 
```
git remote update
```

### Update one repo to another
```
git pull upstream master && git push origin master
```

### Remove permission changes (old mode: 100644; new mode:100755)
```
git config core.filemode false
```

## Fetch a remote PR into your local repo
### Use branch method
```
git checkout -b heshameraqi-master master
git pull git://github.com/heshameraqi/labelImg_OBB.git master

git checkout master
git merge --no-ff heshameraqi-master
git push origin master
```

### Use the PR method (create a PR with the remote PR and your local PR)
```
git fetch origin pull/ID/head:BRANCHNAME
git checkout BRANCHNAME
```

## Add tags for Version Control
```
git tag -a v2.0 beb9829 -m "Deployment v2"
git push origin v2.0
```

## Amend Commits
```
Refer to: https://confluence.atlassian.com/bitbucketserverkb/how-do-you-make-changes-on-a-specific-commit-779171729.html
git rebase -i <Earlier Commit Hash>
Editor will pop up; change "pick" to "edit" for the commits that you would like to change
Examples
git commit --amend --author="jinmingteo <jinmingteo95@gmail.com>" --no-edit 
git commit --amend -m "New Commit Message"
git log
git rebase --continue (confirm your edits and move on to the next commit/edit)

After all the rebase / amendments
git push origin main -f (save the changes)
```

## Rebase fork repo back to main repo
```
git remote add upstream https://github.com/rwightman/pytorch-image-models.git
(git fetch upstream if pull doesn't work)
git pull upstream master
git reset --hard upstream/master
git push origin master --force
```

## Git Loggers
### Full detailed of code changes
```
git log -p
```

### name and status only
```
git log --name-status
```

# Linux Helper

## Sort file size

```
ls --sort=size -lh
```

## Get count (num of files) in the directory
```
ls images/ (will lag)
ls images/ | wc -l
```

## Get directory size
```
du -sh /DATA/jin
```

## Find and **MOVE** txt

```
find . -name '*.txt' -exec mv '{}' /drive/images/ \;
```
## Check PORTS that are in used (IPv4/IPv6)
```
sudo lsof -nP -i4TCP:$PORT | grep LISTEN
```


## Get nohup / other PID
```
ps -ef | grep nohup
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

## Lightweight image viewer
```
feh .
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
tar --use-compress-program="pigz --best --recursive" -cf CityPersons.tar.gz normal_no_rain/ rain/
```

## Download file on Google Drive (GDrive)
```
wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=<FILEID>' -O <FILENAME>
```

# Docker Helper

## Unable to start docker with ```systemctl enable docker```
```
sudo /etc/init.d/docker start
```

## apt-get
```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
   make
```
## CV2 / opencv-python
```
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
    ffmpeg \
    libsm6 \
    libxext6
    
RUN pip install opencv-python
```

## X / QT display issue

```
 xhost +local:docker && docker run --rm -e "DISPLAY=${DISPLAY}" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" <repo>
```

## Unable to write to file </torch_xxx>
```
Either increase shm-size or --ipc=host (will get your sys shm)
docker run -it --gpus all -d -v $dir:/$dir -w $dir --shm-size=256m --ipc=host --expose 8416 -p 8416:8416 mmocr
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


## run.sh required docker-compose environment variables
```
set -o allexport
source docker-compose.env
set +o allexport
```

# Python Helper

## Check site packages
```
python -m site
```

## CPP compilation errors; common.h:124:10: fatal error: Python.h: No such file or directory
```
sudo apt-get install python3-dev
```

## Build wheel on local package (setup.py)
```
# Remove the universal tag if you want to create a Pure-Python Wheel.
python setup.py bdist_wheel --universal 
```

## Check all the linked packages that Python is reading from
```
pip list -v
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

## Check what is in the module
```
from torchvision import transforms
dir(transforms)
```

## Debug console to check variables at that state
```
x = [1,2,3]
i = 3
try:
    x[i] = 100 # code that failed 
except:
    import pdb; pdb.set_trace()
    
# alternatives to pdb
import IPython ; IPython.embed() ; exit(1)

Python 3.7 and above
breakpoint()
```

# Jupyter Helper

## Default Jupyter notebook startup
```
nohup jupyter notebook --no-browser --ip=0.0.0.0 --port 8426 --allow-root > logsfile.logs --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.iopub_data_rate_limit=10000000 & disown
```

## Stop Jupyter notebook
```
jupyter notebook stop <PORT_NUM>
if it doesn't work 
jupyter notebook list
lsof -n i4TCP:<PORT_NUM>
kill -9 <PID>
```


# Pytorch Helper

## Pytorch>=1.6 models not compatible with PyTorch 1.1 or older version
```
# Go to pytorch 1.6 and save model in this way
torch.save(model.state_dict(), path, _use_new_zipfile_serialization=False)
```

# tmux Helper

## Basic tmux panes
```
tmux
ctrl + b + % (vertical split)
ctrl + b + " (horizontal split)
ctrl + b + -> (move to pane to the respective arrowkey)
ctrl + b + x (kill pane)
ctrl + b + ; (go to last active pane)
ctrl + b + c (create another tab)
```

## open tmux when fish is prompted
```
Add new config file ~/.config/fish/conf.d/tmux.fish
if not set -q TMUX
    set -g TMUX tmux new-session -d -s base
    eval $TMUX
    tmux attach-session -d -t base
end
```
