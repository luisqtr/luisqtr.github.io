---
title: Frequent Code Snippets
author: Luis Quintero
date: 2022-11-05 18:00:00 +0100
categories: [notes, dev]
tags: [others]
toc: true
published: true
---

---
# Git

## Git fundamentals

*Based on Course from Corey Schafer on [Youtube.](https://www.youtube.com/watch?v=HVsySz-h9r4&list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx)*

Git is a distributed Version Control System (VCS), SVN is centralized. To check if git is installed use: `git --version`

Initial setup

```bash
git config --global user.name "username" # Same than Github
git config --global
user.email "user@email"		#Same than Github
git config --list 
```

Get help in commands

```
git help <verb>
git <verb> --help
```

## Two common scenarios for Git

### 1. Start tracking an existing project:

``` bash
git init		# Start git tracking
rm -rf .git	    # Stop git (Linux)
rmdir .git		# Stop git (Windows)
git status		# Shows untracked files
```

Create .gitignore file
``` bash
touch .gitignore		    #In Linux-based systems
echo $null >> .gitignore    #In Windows. (Update: DO NOT USE, Wrong encoding)
```

There are three stages:
Working directory, Staging Area, .git directory (Repository).

To add files to the staging area:

``` bash
git add -A		    #Add all files to staging area
git add .gitignore	#Add specific file to staging area

git reset .gitignore #Revert specific file from staging area
git reset		     #Revert all

git commit -m "MESSAGE"	#Commit with a specific message

git log		        #Shows the commit log
```

### 2. Create a remote project in git

`git remote add origin "https://github.com/luiseduve/$repo_name.git"`

Clone remote project that you want to start developing in.

``` bash
git clone <url> <where_to_clone>
git clone ../remote_repo .	#Clone in the current director`
```

View information about remote repository

``` bash
git remote -v	# Information of the repository 
git branch -a	# Branches in the repo locally and remotely
```

When making changes, it is necessary to make pull and then push, to get up-to-date repo:

``` bash
git pull origin <branch>
git push origin <branch>
```

Push all local  branches to the repo, **use carefully**❗❗:

`git push --all `

## Create branches

Common workflow is to create branches instead of working on the `main` branch

```bash
git branch <branchname>		Create branch
git branch				List existing branch
git checkout <branchname>		Work on that branch
```

Shortcut to create and checkout immediately: `git checkout -b <branchname>`

Commit changes as usual on the working branch, it does not have effects on the master or remote branch. Push branch to remote:

`git push -u origin <branch>`

- `-u` associates local and remote branches to be able to use simply git push and git pull

## Merge branches

``` bash
git checkout master
git pull origin master	#In case any changes were made
git branch --merged		#Check which branches have been merged
git merge <branchname>	#MERGE!
git push origin master	
git branch --merged		#Double check that everything was merged
git branch -d <branchname>	#Delete from local repository
git push origin --delete <branchname>	#Delete from origin
```

## Fixing common mistakes in Git

- Remove changes of a file between commit: `git checkout <filename>`

- Modify message of the last commit, this works only in working directory, not with a history where other people has access: `git commit –amend -m "New message"`

- In case we want to move to a branch, the last commit that we accidentally pushed to the master branch: `git cherry-pick <hash from last commit>`

- Try to return to an initial commit, three types: soft, mixed (by default), hard
```
git reset --soft <hash>		# Keep the changes in the staging area
git reset <hash>			# Changes are in the working directory
git reset --hard <hash>		# Reverts all tracked files where it was
git clean -df		        # Reverts untracked files
```

- Even with a reset hard, the `git reflog` and `git checkout backup` can help us to collect back the deleted logs.

- If someone has already worked on the existing commits. `git revert` will create a new commit that undoes the effects of a specific commit hash.

- Untracking a folder that was already committed and now is in the `.gitignore`:
```
`git rm -r --cached <folder_name>/`
`git update-index --assume-unchanged <folder_name>/`
```

-	Update folders based on `.gitignore` changes
```bash
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```

- Track a remote repo from the current local repo: `git branch --set-upstream-to origin/master`

### Stashing temporary changes

``git stash` is useful hen you have changes that you are not ready to commit. Save them in a temporary place and come back to those changes later on:

```bash
git stash save "Message as a reminder"
git stash list	            # List of stash stack
git stash apply stash@{0}	# Take the changes but does not delete it
git stash pop			    # Take the changes and clean the stack
git stash drop stash@{1}	# Delete a stash on the stack
git stash clear			    # Clears the stash stack
```

Stash is shared between branches, then stash can be used to move changes that were done by accident in the master, and commit it in a branch.

## Diff and Merge Tools

Visualize changes between files. Download diffmerge

```bash
git diff 		# Traditional diff
git difftool	# Opens a window with changes
```

## Git submodules

Allow to bring other git repositories (*submodules*) within a main git project (*superproject*)

`git submodule add <GIT URL> [folder name]`

When cloning a repository that has submodules, these submodule folders are empty and need to be checkout:

`git submodule update --init`

To update all the submodules to their respective master branch:

`git submodule update --remote`

Summary of the submodules from the superproject

`git submodule status`

### Keep in mind

- Once your `cd` inside a submodule, all git commands are with respect to the submodule and not the superproject.
- If there is a change in the submodule from the superproject, first you need to `commit` the submodule repo and **then** commit the superproject with a message like `"Update reference to submodule"`. 
- The superproject just keeps a reference to the commit in the submodule that needs to be `checkout`, does **not** track all the changes like it would do to the other folders.


---
---
# Python

## Start a project in Virtual Environments

Create a new virtual environment in the current directory

`python -m venv [env]`
`[env]\Scripts\activate.bat`

Export the packages for the project. After installing the packages, and inside the virtual environment.

```bash
pip list     # Shows the packages that are installed
pip freeze > requirements.txt   # write the packages to a file
```

To load a new virtual environment from the previous requirements

`pip install -r requirements.txt`

Do not commit the `env` to source control, just the `requirements.txt`
To deactivate a virtual environment just deactivate from the `env` folder
To delete a folder with `env`, in Windows: `rmdir venv /s`

Create a venv with access to the system packages:

```bash
python -m venv env --system-site-packages
env/Scripts/activate.bat
pip list
pip list --local # To list just the env packages
```

## Jupyter

### Jupyter-lab

**Note:** Still preferable to use VSCode with their implementation for jupyter notebooks

See installation and docs at <https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html>

This command start in the console and does not trigger the browser automatically:
```cmd
>> start jupyter lab --no-browser`
```

### Convert Jupyter Notebooks to HTML, PDF, $$\LaTeX$$

Install jupyter notebooks from Python pip

`pip install jupyter`

Download and install the program [Pandoc](www.pandoc.org). Requires $$\TeX$$ installation (MiKTeX in Windows) to be able to compile tex files and generate PDF (using XeLaTeX):

To convert a jupyter notebook, run the command window:

`jupyter nbconvert --to <FORMAT> <ipynb file>`

Among the accepted formats there are: `html`, `tex`, `pdf`. For more info about the accepted formats, check [nbconvert website](https://nbconvert.readthedocs.io/)


## Python Unit tests

To test a `calc.py` file with basic calculations. 

Runn the unit test with the normal execution of the file:

`python -m unittest <file>.py`

The contents of a unittest looks as follows:

``` python
import unittest
import calc		# or any other module

class TestCalc(unittest.TestCase):
	
	def setUp(self):
		pass % Executed before every test

	def tearDown(self):
		pass % Executed after every test

	def test_add(self):		% all methods should start with test
		result = calc.add(10, 5)
		self.assertEqual(result, 15)

if __name__ == ‘__main__’:
	unittest.main()
```


## Django App

*Based on tutorials from [Youtube channel](https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p) and [herefor Django and ML](https://www.youtube.com/watch?v=tDnAcbYROSI&list=PLM30lSIwxWOivNtja1_ztft1S_vrMyA0z&index=1)

- Setting up project. After creating a virtual environment

``` bash
pip install django
python -m django –version
mkdir <django_project>
cd <django_project>
django-admin startproject <project_name> .  # Notice the "."
```

To run the server in http://127.0.0.1:8000/:

`python manage.py runserver`

- Create new app using:

`python manage.py startapp <appname>`

- Development of a Django App. Official tutorial [here](https://docs.djangoproject.com/en/2.2/intro/tutorial02/).

Look at the installed apps and create database tables accordingly

`python manage.py migrate`

Look at the classes in `models.py` inside the app and make update migrations:

`python manage.py makemigrations <appname>`

Interactive python to play around with the Django application.

`python manage.py shell`

Create admin user
`python manage.py createsuperuser`

## Create a Python package for publishing

*Overall process based on Isak Samsten presentation*

The packages downloaded through PIP are stored and distributed from pypi.org. Requires an account but is regulated. Usually a package correspond to libraries or machine learning algorithms.

Packages: `setuptools`, `distutils`

### Python packaging tutorial

References to read about packaging:

- https://python-packaging-tutorial.readthedocs.io
- CookieCutter: Better projects template.

### Distribution

Wheel: Binary package in python

Source distribution (sdist) and built distribution (bdist) the packages need to be generic so it can be compiled in multiple platforms

To build binary packages you can use: `cibuildwheel package`

### Cython
Write python code and annotate it so it become more efficient transforming it to C language. Cython 2 allows to call native-C libraries

### Continuous Integration (CI)

Travis: Compiles and test it automatically across different platforms.
Looks for a file .travis.yml that describes how the project is supposed to be built.


---

# OpenSSH

Used to create private and public keys in git repositories hosted outside GitHub, for instance in GitLab/Gitea servers.

SSH protocol provides a secure communication channel to share information with the server without having to provide username and password each time. OpenSSH is the program to generate these keys, which comes by default on GNU/Linux and macOS, but not Windows.

The easiest way is to install either Windows Subsystem for Linux (WSL) or [Git for Windows](https://gitforwindows.org/) which provides Bash emulation (Git Bash) used for running git and the `ssh-keygen` command to create the keys.

Types of SSH keys: Always favor ED25519 SSH keys, otherwise go to common RSA SSH Keys.
More info about security keys [here](https://www.digitalocean.com/community/tutorials/understanding-the-ssh-encryption-and-connection-process)

## Create the SSH key

To create either ED25519 or RSA:

```bash
ssh-keygen -t ed25519 -C "email@example.com"
ssh-keygen -t rsa -b 4096 -C "email@example.com"
```

Flag `-C` adds a comment and helps to identify which is which in case you want to know which is which

Next, input a file path to save the SSH key pair.

Next, you will be prompted to input a password to secure the new SSH key pair. It's a best practice but not required.

To add or change the password of an SSH key pair, use the `-p` flag:

`ssh-keygen -p -f <keyname>`

To add the SSH key to GitLab, copy the SSH to the keyboard using:

*WSL/GNU/Linux (requires xclip package)*

`xclip -sel clip < ~/.ssh/id_ed25519.pub`

*WINDOWS (in powershell)*

`cat ~/.ssh/id_ed25519.pub | clip`

Paste it on the GitLab/Gitea/Github repo in the settings for public keys.

## Test the SSH connection

To test if everything is set up correctly:

`ssh -vT git@<github.com> # Or gitlab.com, or gitea repo`

Finally, clone the repository with git as usual.

## Add the SSH key manually to the agent

- Execute the `ssh-agent` in the git bash console.
- Evaluate `eval "$(ssh-agent -s)"`
- Add the generated key through `ssh-add ~/.ssh/[path_to_key]`

## Persistent use of the same key with known hosts

- Copy and paste both private and public (.pub) keys to `~/.ssh/`
- Create a config file to define which key to use with which host: `nano ~/.ssh/config`
- Add a modified version of this file:
```
Host github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
```

---

# More languages and libraries

## Run local Jekyll website with Ruby

For local debug, install Ruby for Windows as specified on: https://jekyllrb.com/docs/installation/windows/

To install gems and verify that Jekyll is installed
```
>> gem install jekyll bundler
>> jekyll -v
```

To create a Jekyll folder and run the server
```
>> jekyll new myblog
>> cd myblog
>> bundle exec jekyll serve
```

## Git-SVN

For example, the project for TNG-Extreme located in SVN host at DSV.

To clone the repository using Git (i.e. without installing SVN):

`git svn clone svn://svn.dsv.su.se/<user>/<repo> --username=<user>`

Using `git svn` to make changes and commit to svn repository working as a git directory:

```
git svn info
git status
git add -A
git commit -m <message>
git svn rebase --username=<user>
git svn dcommit
```
---
---

