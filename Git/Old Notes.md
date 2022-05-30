# Old Notes

## Documentation from Raji

---

Git structure:

1. Working tree
2. Staging area
3. History area

Git repository structure:  
`` `[team name]`/`[target system]`/`[project name]`/`[code]` ``

> Example:

    trailblazers/salesforce/abc_project/helloworld.cls

### Commands Library

#### Basic Commands

| **Git Command** | **Command Function** |
| --- | --- |
| `git add .` | Add all changed/new/deleted files to the staging area |
| `git commit -m "[commit message]"` | Add files to history |
| `git diff` | Difference between the working tree and the staging area |
| `git diff --staged` | Difference between staging area and history (commit history) |
| `git log` | Show commit history and commit hash |
| ``git rm `[file name]` `` | Remove named file from both working tree and staging area |
| ``git checkout --`[file name]` `` | Reverse the changes of the named file in working tree, and replace with the latest version from staging area |
| ``git reset HEAD `[file name]` `` | Reverse changes of the named file in staging area, replace with the latest version from history area |
| ``git checkout commithash --`[file name]` `` | Restore the named file from an earlier commit to both working tree and staging area |

#### Branch Commands

| **Git Command** | **Command Function** |
| --- | --- |
| ``git branch `[branch name]` `` | Create a new branch with the given title |
| ``git branch -d `[branch name]` `` | Delete the named branch |
| `git branch` | Show all branches |
| ``git checkout `[branch name]` `` | Switch to the named branch |
| ``git merge `[branch name]` `` | Merge the named branch *into* the current branch |

### Initializing a Repository in GitLab and Syncing to Local Machine

1. Create project in GitLab, create master branch and developer branch
2. Go to the project root path, and clone the project path
   - Example: 'https://git.pcfnp.fnni.com/trailblazers/salesforce/yourproject.git'
3. Initialize local folder as Git repository

        git init
        git config --global user.name "[FirstName] [LastName]"
        git config --global user.email [email address]
        git config --list

4. Clone desired branch from GitLab to local machine
   1. Clone from remote repository to local repository

            git clone https://git.pcfnp.fnni.com/trailblazers/salesforce/yourproject.git

   2. Show branches

            git branch

   3. Switch to development branch

            git checkout `[development branch name]`

   4. Checkout code from development branch

            git pull

### Initializing a Local Repository and Syncing to GitLab

1. Create local project with STS
2. Initialize the local project folder as a local repository

        git init
        git config --global user.name "[FirstName] [LastName]"
        git config --global user.email [email address]
        git config --list

3. Create local development branch and switch to it

        git branch [development branch name]
        git checkout [development branch name]

4. Create project in GitLab but do not initialize the repository
   - Example: 'https://git.pcfnp.fnni.com/trailblazers/salesforce/yourproject.git'
5. Add GitLab as a remote repository
   - Example: `git remote add origin https://git.pcfnp.fnni.com/trailblazers/salesforce/yourproject.git`
6. Push code to GitLab

        git push -u origin --all
        git push -u origin --tags

### Push Local Changes to GitLab

1. Check changes

        git status

2. Commit changes to staging

        git add .
        git commit -m "[commit message]"

3. Push changes to GitLab

        git push -u orgin [branch name]

## From Salesforce

---

### One-Time Configurations

| **Git Command** | **Command Function** |
| --- | --- |
| `git config --system` | Access/edit system-wide configuration settings; apply to all users on the computer |
| `git config --global` | Access/edit user-level configuration settings; apply only to user account |
| `git config --local` | Access/edit repository-level configuration settings; apply only to specific repository where set |
| `git config --list` | See config settings for all three levels above |

> Examples of specifying configuration settings:
>
>> | **Git Command Example** | **Command Function Example** |
>> | --- | --- |
>> | `git config --global user.name "[user name]"` | Set username |
>> | `git config --global user.email "[email address]"` | Set user email address |
>> | `git config --global core.autocrlf true` | Set the auto carriage return line feed for Windows |

### Branch Infrastructure

| **Git Command** | **Command Function** |
| --- | --- |
| `git branch` | See a list of local branches |
| ``git branch `[branch name]` `` | Create new branch with given name |
| ``git checkout `[branch name]` `` | Checkout/navigate to new with given name |
| `git status` | Checks status of local branch |
| `git commit -m "[commit message]"` | Commits a change made in working tree to staging tree in local repository with the given commentary |
| ``git push -u `[online repository name]` `[branch name]` `` | Creates remote branch to match named local branch & creates tracking relationship between them |
| `git push` | Can be run after every subsequent push after first time |
| `git pull` | Retrieves all changes from GitHub & updates branch (local) you're currently working on to include changes from remote (combination of two commands git fetch & git merge) |
| `git add --patch` | Add different parts of a file to staging area, helps make commits that are logical units of change |
| `git log` | Access project history; enables display of list of all commits on current branch |
| `git diff` | Helps review changes between last commit of project & various states of files |
| `git revert` | Creates new commit with changes that are the opposite of the commit functionality being undone |
| `git commit --amend` | Make a modification to the last commit you made; will alter the commit history of the project |
| `git reset` | Rewinds history of project, thus also altering the commit history (only use when commits have not been pushed to remote branch) |
| `git rebase` | Creates a fast-forward merge when git would have defaulted to a recursive merge |
