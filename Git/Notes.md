# Comprehensive Notes

## General

---

- `git --version` shows current version of git
- `git update-git-for-windows` updates the version of git
- `git status` checks on status of current repository/working tree
  - Shows branch currently on, whether there any commits to be made, if there have been commits made, etc.
- `git config --list` shows current list of configuration properties like your global user name and email address
  - ``git config --global user.name `[user name]` `` sets global user name
  - Can use `--local` flag to set a name for just a particular git repo if needed
  - ``git config --global user.email `[email address]` `` sets global email address
  - Can use `--local` flag to set an email for just a particular git repo if needed
- `git init` creates (initializes) new git repository in the current working directory
  - Creates .git folder; almost never need to access this folder directly
  - Have to initialize a git repository in a folder/project to be able to use git commands
- `ls` command in git shows current files in local working directory

    > - Can add other parameters to command to view different types of files
    >   - `-c` (cached files)
    >   - `-d` (deleted files)
    >   - `-m` (modified files)
    >   - `-l` (long format, more details about each file)
    >   - `-a` (all files)
    > - Can use multiple parameters by using the letters right next to each other, don't need more hyphens
    > - Adding `` `[character]`*`` will display all files in the directory with names that begin with that character

- `touch` creates a new file in the current repository
  - Example:

        touch index.html

  - `touch .gitignore` creates the git ignore file that will contain all the files we want to omit from commits

## Working with files

---

- To get help on a command, run either line:
  - ``Git `[command]` --help``
  - ``Git help `[command]` ``
- ``git add `[file names]` `` adds files to the staging area/index to be committed
  - Need to include file extensions with file names
  - Don't need to comma-delimit; just separate with spaces
  - Just `git add .` will add all new or modified files to staging area
  - ``git add *.`[extension type]` `` will add all files of that extension to the staging area
  - Example:

        git add *.html

  - `git add -A` adds all files
- `git commit` pushes files to the repository that have been staged
  - Can add other parameters to command such as `-m "[commit message]"` as a memo for the commit
    - This allows you to skip a weird edit stage with an unintuitive interface -- VIM
        > If you get there, press "Esc" and then type ":wq!" to write, quit, and save; or press "i" to enter insert mode and make changes
  - `git commit --amend --no-edit` will update the hash and timestamp of the most recent commit without making any changes to files or requiring message dialog
  - `git commit --allow-empty -m "[commit message]"` sends an empty commit to the repository
  - `-a` flag will automatically stage and commit any new/modified files in the staging area within a commit command
    - `git commit -a -m "[commit message]"`
        > (don't need to do the git add command if running this command)
- ``git rm --cached `[file name]` `` will remove a file you specify back out of the staging area, without committing it
  - file becomes "untracked" once again
  - ``git reset `[file name]` `` will also do this
- ``git rm `[file name]` `` will remove a file from a git repo and the file system
  - Change is made in the working tree, and moves the deletion to the staging area. Commit the change to finalize it in the repo
  - Adding `-r` will enable recursive delete, allowing you to delete a folder and all of its contents in one `rm` operation
- `rm -rf .git` removes a git repository from inside a local folder
- `git diff` returns any differences in files not yet committed/pushed
  - Run `git diff --staged` to see all the changes in files that are new or modified in the staging area
    > Shows diff between staging area and most recent commit
- If a change is made to a file and the file has not been added to the staging area yet, you can back out of that change by running the command ``git checkout --`[file name]` `` to revert the change made on the file back to its state in the staging area
  - Must be done ***before*** the file is added to the staging area with `git add`, and overwrites the last staged version
  - Changes rolled back in this way can't be recovered since they were never added to the staging area/committed, and thus aren't part of the git history
- ``git reset HEAD `[file name]` `` will remove a file that has been added to the staging area and place it back in the working tree; will go back to being just a tracked file with changes
- ``cat `[file name]` `` will show the contents of a text file you specify
- `git stash` allows you to "save" changes made to file(s) on the current branch without committing them so you can switch to another branch without losing recent changes made to any file(s)
  - `git stash list` shows currently stashed changes on current branch
  - Add `-p` to show edits made for each stash
  - `git stash apply` reapplies/reverts changes to file saved in the most recent stash
  - To apply a specific stash, include the label of the stash at the end of the command

    ![Git_Notes_image1.png](/Resources/Image%20Resources/Git_Notes_image1.png "example of git stash from netauto project")

  - Add a helpful message to a stash point by running git stash save "stash message"

## Branching Strategy

---

- ``git checkout `[commit hash]` `` will revert to the state of a previous commit
  - Obtain the commit hash using `git log`
  - The hash is the long string of characters and numbers
  - Checking out a hash actually redirects you to a different branch created to view that old, previous state of your project
  - `git checkout master` or ``git checkout `[whatever branch you were on before]` `` will take you back to the branch you were on before
  - ``git checkout -b `[new branch name]` `[basis branch name]` `` will create a new branch and check it out, and base it upon another branch you optionally specify
    - Basis for new branch will default to the branch you're currently on, so not necessary if creating off of that branch
  - ``git checkout `[5-character beginning of commit hash ID]` --`[file name(s)]` `` can restore a previously discarded file from a commit where it was present
- `git checkout <other-branch-name> -- <file-name>` will checkout a file from another branch to the local branch you're currently on
- `git branch` will list out all existing branches
  - ``git branch `[new branch name]` `` will create a new branch from the current branch you're on with the name you specify
    - Will essentially clone the branch you're on, at the same point in time regarding your commit status
  - Try `git branch -a`
  - `git branch --merged` will show all branches that have been merged between local & online repositories (into master branch..?)
    - Lets you know that redundant/obsolete lower-level branches are safe to be deleted
  - ``git branch -d `[branch name]` `` will delete a branch locally that you specify
    - Can only delete branches that are merged, show up under the results of `git branch --merged`
    - To hard-delete unmerged branches (not recommended), run ``git branch -D `[branch name]` ``
- ``git merge `[branch name]` `` will merge the branch you're on into the branch name you specify
  - Can also add a merge message with `-m`
- `git push` pushes local repository you're working in to a remote repository, like GitHub
  - ``git push -u `[online repository alias]` master/`[other local branch name]` `` will push the master (or other) branch from your local repository to your online repository
  - Can push multiple branches to a remote repository at a time; space-delimit them, no commas
    - Alternatively, can run ``git push `[online repository alias]` --all`` to push all branches to the remote repository at once
  - Will need to provide credentials to remote repository at this time
    - Alternatively, can create SSH keys with GitHub
  - Once your online repository has been authenticated/linked you can promote committed changes to it with a simple `git push` command
  - ``git push `[online repository alias]` --delete `[branch name]` `` will delete a branch you specify from the online repository
  - ``git push `[online reposotiry alias]` -u `[new branch name]` `` will push a newly named local branch to your remote repository if you've just locally renamed a branch (see how to rename a local branch below)
- `git pull` pulls latest changes from a remote repository to your local repository
  - Always do a git pull before a git push so you don't lose changes others might have made since you last did a git pull from the remote repository!
  - Include alias of online repo (without "-u") and branch name directly after "git pull"
  - Example:

        git pull online_repository_alias master

  - Adding `--allow-unrelated-histories` after the remote repository alias & remote branch name will allow you to pull in a remote project to your local repo if you get an error about there being unrelated histories (tread lightly...)
- `git fetch origin master ; git merge origin/master` will accomplish the same thing as `git pull origin master`
  - The separation of steps lets you do a git status command after the fetch command and before the merge command to see the changes between the online files and local files before you merge them into your local repository
- `git clone` pulls a remote repository into your current folder in a new directory; pulls all files from a directory (remote or local) into another directory
  - Syntax: ``git clone `[online repository URL]` `[location to clone repo]` ``

    > location specifier is optional; will default to current file directory path

  - Use `.` for the location to clone to use the current directory that you're in
  - Example:

        git clone https://github.com/[your_username]/[your_online_repository].git 

  - Can't clone a git repository into another repository; make sure you run a git status command and no repository comes up for the folder you're currently in
- `git remote` lists all available remote repositories (if you've linked any)
  - Try `git remote -v`
  - ``git remote add `[online repository alias]` https://github.com/`[your_username]`/`[your_online_repository]`.git`` adds an online repository for your project by the alias you specify
  - Now the online repo will show up with the alias you provided it when you run git status
  - Can add additional online repositories to the same local repository; just have to specify which one pushing changes to when you do a `git push`
  - Can switch the default remote repository for push commands by adding `--set-upstream` before the online repository tag in a `git push`
  - Example

        git push --set-upstream second_online_repository_alias master

- ``git remote rename `[current remote repository name]` `[new remote repository name]` `` will change the name of a remote repository in a git project on your local machine
- ``git branch -m `[old branch name]` `[new branch name]` `` renames a local branch in your local git repository
- ``git diff `[branch 1]`..`[branch 2]` `` will show the differences between two branches directly related in the branching tree

## Terminal Commands

---

- `clear` will clear the history/previous commands run on the terminal

> Ctrl commands in Bash:
>
> - **Ctrl + A** sends cursor to beginning of line
> - **Ctrl + E** sends cursor to end of line
> - **Ctrl + U** deletes everything before cursor
> - **Ctrl + K** deletes everything after cursor
> - **Ctrl + L** clears terminal/command history (like clear command)
>   - But unlike clear, ctrl + L keeps what's on the line currently while still clearing history

- Can include multiple commands in one line in bash terminal, separating commands with a semicolon
- `git log` provides a history of commits
  - Add `-p` to show exactly what changes were made to which files in the git repository
  - Add ``--author=`[author name]` `` to show commits made from exactly one author (based on git user name)
  - Press `q` to exit the long-form of git log in the terminal
- Can create shortcut commands in git session with `alias` command
  - Such as, making a nice commit graph command instantly accessible by running a command like `alias graph="git log --all --decorate --oneline --graph"`
- **Ctrl + Ins** copies in the terminal, **Shift + Ins** pastes in the terminal
  - When pasting, it will automatically execute command, so surround it in quotes if you don't want to execute right away

## Other Git Notes

---

- Include the names of files you want to exclude from commits/adds in the .gitignore file
  - Example of what contents of .gitignore should look like

        log.txt
        ignorethisfile.js
        ignorethisfilletoo.css
        *.xlsx
        ... etc.

  - Can add whole directories (folders) to .gitignore by prefacing the folder name with a `/`
  - Add all files of a certain extension type by using an asterisk before that extension type in .gitignore
- Git/github are separate entities
  - Git = version control language, keep track of changes to files/projects
  - Github = allows sharing projects/repositories with team members, publish things online, collaborate on open-source projects, etc.
  - Git is main technology, github is platform to collaborate/share it
- 1st use case: you have a project/repo on your local machine, you want to push it to Github
- Fork button in Github creates your own copy of an open source project; clones the repository to your own account
  - Then you can clone your own copy that you forked instead of cloning the original
  - Clicking pull request button will allow you to create a pull request to commit changes you made in a local copy of a forked repo back to the original repo you copied

> **Workflow**:
>
> - Create new branch
> - Check out new branch
> - Edit files in project
> - Git status
> - Git add changes to staging directory
> - Git commit
> - Git push origin branch name
> - Git checkout master
> - Git pull origin master
> - Git merge new branch
> - Git push origin master

- In git, **HEAD** is a pointer that normally points to a branch, and not a commit
  - **HEAD** tells us what we have checked out
- New branches are always instantiated where the **HEAD** pointer is
