# Directory
## [Git HelpDesk](#git-helper)

## [Mac Linux HelpDesk](#mac-linux-helper)

## [Docker HelpDesk](#docker-helper)

## [Kubernetes HelpDesk](#kubernetes-helper)

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

### Rename branch
```
git branch -m <newname>
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

#### rename branch
```
git branch -m <old_branch> <new_branch>
git branch -m feat/yoyoyo feature/yoyoyo
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

### squash commmits
```
# goes back 3 commits
git rebase -i HEAD~5 

# proceeds to interactive vim mode
# fixup the commits to initial commit / following command change pick to fixup
:%s/pick/fixup/g 

should look something this
pick commit_1 / edit commit_1 / reword commit_1
fixup commit_2
fixup commit_3

git rebase --continue
git push origin master -f 
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

# just editing files
git add -u
git commit --amend --no-edit

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

## Rebase / Update old branch with master
```
# get latest master, go to branch and rebase to it.
git checkout master
git pull
git checkout custom-branch
git rebase master
git push origin -f custom-branch
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

# Mac Linux Helper

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

## Get directory size recursively
```
du -h --max-depth=1 /DATA2/jin | sort -rh
```

## Find and **MOVE** txt

```
find . -name '*.txt' -exec mv '{}' /drive/images/ \;
```

## peek file (top/bottom 10 lines)
```
head -10 image_list.txt
tail -10 image_list.txt
```

## kill all tail programs
```
ps aux | grep '[t]ail' | awk '{print $2}' | xargs kill
```

## diff directories
```
# exlude .git directory
diff --exclude=.git -qr folder/ folder-old/
```

## Check PORTS that are in used (IPv4/IPv6)
```
sudo lsof -nP -i4TCP:$PORT | grep LISTEN
```

## Get nohup / other PID
```
ps -ef | grep nohup
```

## Get all nvidia-smi processes and respective directory
```
sudo pwdx `nvidia-smi -q -x | grep pid | sed -e 's/<pid>//g' -e 's/<\/pid>//g' -e 's/^[[:space:]]*//'`
```

## Kill python

```
pkill -9 python
```

## Kill previous job
```
kill %%
```

## Copy directory with symbolic link
```
// -r is recursive; -l is --dereference
cp -R -L . /DATA/output 
```

## Copy and Rename images in a directory
```
for i in *.jpg; do scp -p "$i" "../images/MOT17_11_`echo "$i" `"; done
```

## Convert mp3 to wav
```
ffmpeg -i {mp3} -acodec pcm_s16le -ar 8000 {wav_file}
```

## Compress video
```
## where 0 is lossless, 23 is default, and 51 is worst possible.
 ffmpeg -i foo.avi -vcodec h264 -an foo.mp4
 ffmpeg -i video_12_02_2024.mp4 -vcodec libx264 -crf 24 12_02_2024.mp4
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

## Commit (hacky; only use for quick testing
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
docker commit e5ef0 helloworld-container
docker push helloworld-container
```

## X / QT display issue

```
 xhost +local:docker && docker run --rm -e "DISPLAY=${DISPLAY}" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" <repo>
```

## Unable to write to file </torch_xxx>
```
Either increase shm-size or --ipc=host (will get your sys shm)
docker run -it --gpus all --name mmocr -d -v $dir:/$dir -w $dir --shm-size=256m --ipc=host --expose 8416 -p 8416:8416 mmocr
```

## RuntimeError: DataLoader worker (pid 1124261) is killed by signal: Bus error. It is possible that dataloader's workers are out of shared memory. Please try to raise your shared memory limit.
```
# check /dev/shm (usually should not be full)
df -h

# check which program is hogging /dev/shm (have to stop; deleting files won't work if process is using)
lsof /dev/shm (processes that are using /dev/shm)

# cached / files in the directory
ls -lh /dev/shm
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

- Run Docker as root
```
docker exec -u 0 -it mycontainer bash
```

## run.sh required docker-compose environment variables
```
set -o allexport
source docker-compose.env
set +o allexport
```

# Kubernetes Helper
```
kubectl ingress pods -n <namespace>
kubectl get pods -n <namespace> 
kubectl get deploy -n <namespace> serviceexample -o wide

kubectl describe pods -n <namespace> serviceexample-5696958c86-4t5kx
kubectl describe deploy -n <namespace> serviceexample
kubectl describe node <name> -n <namespace>

kubectl get nodes --show-labels | grep g54x
kubectl top nodes -l spr-cluster=g54x

# get generic nodeSelector
kubectl get pods -n <namespace> --field-selector=status.phase=Running -o custom-columns=POD:.metadata.name,NODE:.spec.nodeSelector | grep generic 
```

## Replicaset
```
kubectl logs -f serviceexample-5696958c86-4t5kx -n <namespace>
## trace how previous container died
kubectl logs -f serviceexample-5696958c86-4t5kx -f <release_name> --previous -n <namespace> 
```

## combined output
```
kubectl logs -f serviceexample-5696958c86-4t5kx -c serviceexample -n <namespace>
```

## get nodes type / description
```
kubectl get nodes -o wide -L beta.kubernetes.io/arch -L beta.kubernetes.io/os -L beta.kubernetes.io/instance-type -L kops.k8s.io/instancegroup -n <namespace>
```

## Check what is in the node
```
kubectl get pods -o wide -n intuition --field-selector spec.nodeName=<env>-<namespace>-node-202211190856-1617-z100   
```

# Python Helper

## List comprehension
```
[x+1 if x >= 45 else x+5 for x in xs]
[x+1 for x in xs if x>=45]
```

## Check site packages
```
python -m site
```

## CPP compilation errors; common.h:124:10: fatal error: Python.h: No such file or directory
```
sudo apt-get install python3-dev
```
## Cmake errors / upgrade 
```
# apt-get install might not give the latest version.
pip install cmake --upgrade
```

## Build wheel on local package (setup.py)
```
# Remove the universal tag if you want to create a Pure-Python Wheel.
pip install wheel
python setup.py bdist_wheel --universal 
```

## Check all the linked packages that Python is reading from
```
pip list -v
```

## pip install locally (assuming there is setup.py on directory)
```
pip install -e .
```

## Create venv
```
virtualenv -p python3 venv/
source venv/bin/activate
```

## Clone conda environment
```
conda create --name cloned_env --clone original_env
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

## Check where is the module from
```
import torch
torch.__file__
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

## Check text diff on jupyter notebook
```
import diff_match_patch as dmp_module
from IPython.display import display, HTML

dmp = dmp_module.diff_match_patch()
diff = dmp.diff_main("Hello World.", "Goodbye World.")
dmp.diff_cleanupSemantic(diff)
display(HTML(dmp.diff_prettyHtml(diff)))
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
lsof -n i4TCP:<PORT_NUM> / ps aux 
kill -9 <PID>
```

## Add conda env to notebook
```
<at_my_env>
conda install -c anaconda ipykernel
python -m ipykernel install --user --name=<at_my_env>
```

# Tensorboard

## Default Tensorboard startup
```
nohup tensorboard --logdir=. --port=8417 --host=0.0.0.0 & disown
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

# screen Helper
```
screen -ls
screen -S {name}

## get out of screen
ctrl + a + d

## resume screen
screen -r {name}
```
