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
2. Add files to git stagging area by typing `git add .` 
* You can use the '.' as a wild card that means all files in directory
3. Commit with the core editor by typing `git commit` 
* This will bring up Sublime text and you can type your commit message instead of writing it on the command prompt

#### Express Commits
* To list all files being tracked type `git ls-files`
1. Type `git commit -am "Commit Notes"`
* The '-a' command tells git to add modify files to get stagging area 
* We're adding a modifying file to the stagging area because that's how git works. But really we are adding the modification of the file to the stagging area. 

#### Backing Out Changes By Unstagging from Stagging Area
* If you added changes to your stagging area but would like to back out of them and revert to the most recent commit: 
* Type `git reset HEAD [file name]` this will reset the changes in the stagging area. Meaning nothing will be deleted or lost but the file changes will not be in the stagging area anymore
* To discard the changes entirely and return to the last known good state of the file:
* Type `git checkout -- [file name]`

#### Git History and Making New Commands with Alias
* Type `git log` to view commit history
* Type `git help log` to get information about different types of log commands
* Type `git log --online --graph --decorate --all`
* Create a git Alias, which is basically a new command that is a abbraviated of existing git commands
1. Type `git config --global alias.hist "log --online --graph --all"`
* The syntax is:
** Write to git config file
** Pass '--global' to make it a global alias
** Name the alias command, so 'alias.hist' where 'hist' is the command
** Type the git command in quotes - "log --online --graph --all"
2. Verify that the command has been entered by checking the git config global list:
* Type `git config --global --list`
* You should see the alias at the bottom
3. To use an alias, type `git [alias name]`

#### Rename and Delete Files
* To rename a file in a git repo type `git mv [filname] [new filename]`
* By using a git command, you will track the changes to the file name and Git will reconize that it's the same file but just renamed
* To delete a file in a git repo type `git rm [filename]` 
* Using the git command to delete a file will automatically track the changes  

#### Managing Files Outside of Git
* You created new files using a bash command (`subl example.txt`) in a git repo 
* Or you renamed files using the `mv example.txt example_2.txt` 
* Git will see the new files as untracked and also see the renaming of a file as a deletion and adding an untracked file. You will need to tell git about those changes 
* In order to include BOTH deletions and additions you need to use `git add -A` 
* If you wanted to delete a file in a git repo using a bash command `rm [filename]` you will need to update those changes to the stagging area. 
* To stage a deleted file from the bash command type `git add -u` '-u' means update

#### Excluding Unwanted Files
* To exclude unwanted files from a git repo, you will need to create a gitignore file that list the unwanted files 
* Type `subl .gitignore` to create the git ignore file in the repo
* The syntax is just one file name per line. For example, log.txt
* You can use wildcards such as `*.log` to ignore all log files
* Stage and commit the .gitignore file

## Advanced: Beyond the Basics
#### Comparing Differences Using Diff
* Type `git hist` to get a tree log of all of the commmits and their ids
* To see differences between two commit points, type `git diff [commit id] [HEAD]` You will see the difference between that commit id and the HEAD.
* To use the diff tool, p4merge, type `git difftool`
* To get help on the diff command, type `git help diff`
* Any parameter that can be passed in a `git diff` command can be passed using the difftool

#### Branch and Merge Types
* Branching is a timeline of commits
* Branch are the names or labels to timelines in git 
* You can create or delete branches without affecting timelines because all you are doing is creating or deleting labels of commit ranges in git
Types of Merges:
1. Fast-Forward Applied:
* Simple and straight forward
* Happens in the simplest of cases when no additional work has been detected on the master branch. 
* Git will apply all commits on the other branch to the parent or master branch as if you didn't branch off to begin with
2. Automatic: 
* Happens when git detects non-conflicting changes on the parent branch
* Git will automatically resolve any conflicts 
* Perserves both branches (timelines)
3. Manual:
* Happens when git is unable to resolve all of the merge conflicts
* Git enters a Conflicting Merge State
* Automatic merging not possible
* Changes are saved in a Merge Commit

#### Special Markers
* HEAD
* Points to the last commit of the current branch
* HEAD is normally the last commit of the current branch
* As you switch branches HEAD moves to be at the last commit location of that branch 

#### Branching A Fork In Time
* Use feature or topic branches in order to seperate out changes that you want to make off of the master branch
* To see the branch you are on, type `git branch`
* To create and switch to new branch type `git checkout -b [branch to create]`
* Creating a branch is good if you want to isolate new features from the master branch. You can carry over modified or unstaged changes into your new branch from master. 
* You can see the differences in branches by using the difftool or diff command and passing in the names of the branches to compare. For example, type `git diff updates master` to compare updates branch to master 
1. To inegrate changes on a feature branch you need to first switch back to the parent branch, which is master. Type `git checkout master`. The checkout command allows you to switch between branches
2. `git merge [branch name to merge]` to merge (fast-forward merge) branch to master
3. Since branches in git are just labels of timelines, once you integrate a branch into the main timeline, you will want to remove the extra branch. Type `git branch -d [name of branch to delete]`
4. Type `git branch` and `git hist` to check the branch and updated history

#### Stashing - Save Temporary Changes
* If you're in the middle of working on a file and need to switch to work on something else, but are not ready to commit your changes, you can "stash" the work. 
1. type `git stash` which will save the last commit and any modified files into a "work in progress" area on master
2. type `git stash list` to see a list of your stashes
3. After the stash you are back on a clean work directory and are able to work on something else 
4. Edit the files that you need to and when you're done do a git commit
5. Verify that you are back to a working directory with a git status and then apply the stash 
6. type `git stash pop` The 'stash' will apply whatever the stash is and then the 'pop' will drop the stash that was applied. Now you can continuing working and then commit your changes. 

#### Reset and Reflog
NEED TO UPDATE


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







