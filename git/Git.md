# **Git to Know**

-  Version Control System

- Distributed VCS

- Every user clones a copy of a repository

- This clone has all of the metadata of the original while the original itself is stored on a self-hosted server or github

- It also synchronise code between multiple people working on the same project

- Repository: a collection of source code

  

![Gitworkflow](Gitworkflow.png)

## Three States

| State     | Feature                                                      |
| --------- | ------------------------------------------------------------ |
| Staged    | the files with the updated changes are marked to be committed to the local repository but not yet committed |
| Modified  | the files with the updated changes are not yet stored in the local repository |
| Committed | the changes you made to your file are safely stored in the local repository |

## Git Commands

| Command    | Function                                                     |
| ---------- | ------------------------------------------------------------ |
| git add    | to add a file that is in the working directory to the staging area |
| git commit | to add all files that are staged to the local repository     |
| git push   | to add all committed files in the local repository to the remote repository |
| git fetch  | to get files from the remote repository to the local repository but not into the working directory |
| git merge  | to get the files from the local repository into the working directory |
| git pull   | to get files from the remote repository directly into the working directory. It is equivalent to a `git fetch` and a `git merge` . |

## Git Installation

```bash
#Version Check
git --version 

#installing in Linux
sudo apt install git-all

#for Windows go to this link
https://gitforwindows.org/
```

## Git Configuration

```bash
#Authorization
git config --global user.name "YOUR_USERNAME"
$ git config --global user.email "myemail@gmail.com"

#To Check the info you provided
git config --global --list
```

**NOTE**

From August 13, 2021, GitHub is no longer accepting account passwords when authenticating Git operations. You need to add a **PAT (Personal Access Token)** instead, and you can follow the below method to add a PAT on your system.

- Step 1: [Create a Personal Access Token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token) 

- Step 2: For Linux-based OS

  Once GIT is configured, we can cache the given record in your computer to remember the token

  ```bash
  # For Linux, you need to configure the local GIT client with a username and email address
  $ git config --global user.name "your_github_username"
  $ git config --global user.email "your_github_email"
  $ git config -l
  
  #Once GIT is configured, we can begin using it to access GitHub. Example:
  $ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
  > Cloning into `Spoon-Knife`...
  $ Username for 'https://github.com' : username
  $ Password for 'https://github.com' : give your personal access token here
  
  # Now cache the given record in your computer to remembers the token:
  $ git config --global credential.helper cache
  
  # If needed, anytime you can delete the cache record by:
  $ git config --global --unset credential.helper
  $ git config --system --unset credential.helper
  
  #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
  ```

  For other OS follow this [article](https://stackoverflow.com/questions/68775869/support-for-password-authentication-was-removed-please-use-a-personal-access-to)

## Using GitHub with SSH Key (optional)

- Why SSH? You can connect and authenticate to remote server and services, without supplying your username and personal access token at each visit. [Learn more](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/about-ssh)

- Before you generate an SSH key, you can check to see if you have any existing SSH keys. [Learn more](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

  ```bash
  # Lists the files in your .ssh directory, if they exist
  ls -al ~/.ssh
  ```

- Generating SSH key and adding it to the ssh-agent [Learn More](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

  ```bash
  #Generating a new SSH Key
  ssh-keygen -t ed25519 -C "your_email@example.com"
  
  #Starting the ssh-agent in the background
  eval "$(ssh-agent -s)"
  
  #Adding your SSH Key to the ssh-agent
  ssh-add ~/.ssh/id_ed25519
  ```

- Adding a new SSH Key to your GitHub account [Learn More](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

  ```bash
  # Downloads and installs xclip. If you don't have `apt-get`, you might need to use another installer (like `yum`)
   sudo apt-get update
   sudo apt-get install xclip
  
  # Copies the contents of the id_ed25519.pub file to your clipboard
   xclip -selection clipboard < ~/.ssh/id_ed25519.pub
  ```

- Testing your SSH connection [Learn More](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/testing-your-ssh-connection)

  ```bash
  # Attempts to ssh to GitHub
  ssh -T git@github.com
  ```

## Let's Git

- Create a Repository
- Go to your working directory

### Initialize Git

```bash
 # To create a README file for the repository
 touch README.md
 
 # Initiates an empty git repository
 git init          
```

### Add files to the Staging Area for commit

```bash
# Adds all the files in the local repository and stages them for commit
git add . 

# To add a specific file
git add README.md 
```

### Git Status

```bash
# Lists all new or modified files to be committed
git status
```

### Commit Changes to Local Repo

```bash
# The message in the " " is given so that the other users can read the message and see what changes you made
git commit -m "First commit"
```

### Remove file from staging area

```bash
# to remove all files from the staging area
#-r is used for recursive 
git rm --cached -r .
```

### Uncommit Changes you just made to your Git Repo

```bash
# Remove the most recent commit# Commit again!
git reset HEAD~1
```

- Reset can be --soft, --mixed, --hard. [Learn More](https://levelup.gitconnected.com/confused-with-the-difference-between-git-reset-soft-mixed-hard-3285e8b5cd0f)

![GitReset](gitreset.png)

### Add a remote origin and Push

```bash
# sets the new remote
git remote add origin remote_repository_URL

# Use this if you have enabled SSH
git remote add origin git@github.com/satishkarki/Notes.git

# Use this if SSH is not enabled
git remote add origin https://github.com/satishkarki/Notes.git

# List the remote connections you have to other repositories
git remote -v

# pushes changes to origin
git push -u origin main 
```

**NOTE**

On Oct. 1, 2020, any new repositories you create will use main as the default branch, instead of master, It is GitHub's effort to remove unnecessary reference to slavery and replace them with more inclusive term.

### Removing Remote Repository

```bash
# View current remotes
git remote -v

> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
> destination  https://github.com/FORKER/REPOSITORY.git (fetch)
> destination  https://github.com/FORKER/REPOSITORY.git (push)

# Remove remote
git remote rm destination

# Verify it's gone
git remote -v

> origin  https://github.com/OWNER/REPOSITORY.git (fetch)
> origin  https://github.com/OWNER/REPOSITORY.git (push)
```

**Note**: `git remote rm` does not delete the remote repository from the server.  It simply removes the remote and its references from your local repository.

### See the changes made to your file

```bash
# To show the files changes not yet staged
git diff 
```

### View Commit History

```bash
git log
git log --oneline --graph
```

## Basic Git Flow

```bash
git add .

git status # Lists all new or modified files to be committed

git commit -m "Second commit"

git push -u origin main
```

## Cloning a Git Repo

```bash
git clone remote_repository_URl
```

## Git Ignore

When we push our source code in the remote repository then we can use git ignore to exclude sensitive files likes API keys, passwords and even the local setting files, which is just local to our settings. One example of unwanted file is DS_Store file. 

- You can get pre-built template for gitignore file from this [repository](https://github.com/github/gitignore)

```bash
# Create a .gitignore file
touch .gitignore

# Add file to be ignored in .gitignore file
vim .gitignore

#Then list the files you want to ignore as a list, Example
.DS_Store
API/api.html
```

## Collaboration

![GitWorkFlow](gitworkflow.png)

### Branching and Merging

![branch/merge](branchmerge.png)

```bash
# Create a branch
git branch blue

# List the branch, * sign shows the current branch we are in
git branch

# Let's say you are in main branch and wants to go to blue branch
git checkout blue

# If I want to merge the blue branch again with the main 
git merge blue
```

### Forking and Pull Request

![forking](fork.png)

If you want to learn more about the Git Branching...[go to this site](https://learngitbranching.js.org/)

## References:

- https://www.udemy.com/course/the-complete-web-development-bootcamp/

- https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/

- https://www.toolsqa.com/git/difference-between-git-clone-and-git-fork/

  
