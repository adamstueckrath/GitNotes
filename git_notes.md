# Git and GitHub Notes 

## Core Concepts
#### What is Git
* A decentralize or distrubuted version control system 
* Most people decide to use a central server for work
* Able to scale massively
* Most operations are local and super fast
* Open source and free

#### The Repository 
* Collection of files managed by Git
* History of everything
* Working directory/workspace can contain both files contained by git and other files and folders that are excluded from version control or not managed by Git
* Every Git Repository will contain a .git folder that contains the actual repository
* Keep repositories seperate and focused. For example, a repo for the front-end and back-end for an application 

#### Commits and Files
* Git works by saving the current state of all it's managed files in snapshots, called Commits
* A commit can contain one or more file changes 
* Git versions files not folders
* Can create dummby files to save a folder in Git
* As you make changes Commits are saved on a timeline called a Branch
* A Git repository will only have 1 branch by default that branch is called Master

## The Basics
#### Create a Git Repository Locally
1. cd into directory you would like to create a git repo
2. type `git init folder-name`

#### Git States
Local Git States:
1. Working Dirctory 
Contains all files and folders for your application 
2. Staging Area
Area in between working directory and repo. Its used to prepare for the nexts commits  
3. Repository (.git folder)
Contains all commits or changes to the git repository 
4. Remote - another repository 

#### Working Through the Git States
* type `git status` to receive the status of the current working branch 
1. To move files from the working directory to the stagging area:
* Type `git add [file name]`
* You can verify files in the stagging area by using the git status command 
2. To move files from the stagging area to the git repository:
* Type `git commit -m "Commit message"`
* You can verify the commit by using git status and seeing if the working directory is clean 

#### Adding Git to Existing Project
1. Type `git init .`
* You need to be in the working folder to use '.' operator or else cd out and use `git init folder name`



## Advanced: Beyond the Basics

## SSH Authentication 
#### Generating an SSH Key
1. Create a directory called `.ssh` in your user home directory (/Users/adamstueckrath)
2. type `mkdir .ssh`
3. change directory (cd) into .ssh
4. type `ssh-keygen -t rsa -C "stueckrath.adam@gmail.com"` 
* the `-t` means type, and `-C` means common name
5. press enter to save the id_rsa file in the .ssh dir
6. create a passphase and verify it
7. type `ls -al` to verify that you have created the ssh keys 
8. the .pub file is your public key and the one without is your private key

#### Verify SSH Authentication with GitHub
1. Open your id_rsa.pub file and copy the contents 
2. Open GitHub and navigate to your profile settings
3. Open your SSH and GPG Keys settings and click 'New SSH Key'
4. Enter a title and paste in your id_rsa.pub file contents
5. Next type `ssh -T git@github.com` 
6. Type yes to continue connecting
7. Enter your ssh key passpharse 
* ssh should connect and you should see your github username  in the terminal

## GitHub Repository
#### Create a Local Copy with Clone
1. Type `git clone git@github.com:adamstueckrath/my-website.git`
* When doing a git clone command, by default git sets up origin to be the name of the remote reference
* If you type `git remote -v` you will see "origin" pointing to back to github
2. If you want to clone a repository with a different folder name, type `git clone git@github.com:adamstueckrath/my-website.git website`

#### Seeding the Repository with Sample Content
1. Go to initializr.com to get started with a website template 
2. Type `cp -R ~/Downloads/initializr/* .` to copy the template files into the website folder 
* The '-R' means recrusive, the star means wildcard, and the '.' means copy to current folder
3. Track the files with git by using `git add .` 
* The star means all untrack files in current folder
4. Commit files by typing `git commit -m "Adding initial website files"` 
5. Push new files to github, type `git push origin master`
* First parameter in push command is the name of the remote reference (origin).
* Second parameter is the branch name (master)

#### Publish Back to GitHub
1. Set default push behavior, type `git config --global push.default simple`

#### Difference Between Fetch and Pull
1. `git fetch` are non-destructive
2. git pull or fetch prior to any pushes is the best practice 
3. Review good information when working with others!

#### Updating Repository and Remote Reference
* Lets say you want to udpate your repository name on github from "my-website" to "website"
* You need to now point the remote origin reference to "website" instead of "my-website"
1. Type `git remote -v` to see the remote reference information 
2. To update the remote reference type `git remote set-url origin git@github.com:adamstueckrath/website.git`
3. Type `git remote -v` to verify changes
4. To get additional information about origin type `git remote show origin`

#### Synchronizing GitHub Changes with Local Repository
* If you make changed on GitHub, you want to update your local repository with those changes 
1. Type `git fetch` to update the references from github
2. Type `git pull` to fast-forward and update the local branch 


## GitHub Repository Branches 
#### Creating Branches on GitHub
1. Not best practice. Better to create locally and then push to github
2. Type the branch name under the Branch dropdown and hit enter 

#### Creating Local Branches
1. Type `git checkout -b 'branch name'`
2. Push branch to github, type `git push -u origin branch name`


#### Merging Locally
1. Check out 

#### Locally Switch to a Branch on GitHub


#### Cleaning Up By Deleting Branches and References









