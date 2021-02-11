# Milestone #1 - Get that Code

```
$ git clone <add-ssh-link-here>
```

```
$ git remote -v
origin  git@gitlab.crio.do:COHORT_ME_GIT_BASICS_ENROLL_1596802014715/chauhanachiv-ME_GIT_BASICS.git (fetch)
origin  git@gitlab.crio.do:COHORT_ME_GIT_BASICS_ENROLL_1596802014715/chauhanachiv-ME_GIT_BASICS.git (push)
```

```
$ git status
On branch master
Initial commit
nothing to commit (create/copy files and use "git add" to track)
```
### Q. When would you need multiple remotes?
* If we need to fetch files from a different repository other than the one we cloned from, new remotes should be added for these repositories using the `git remote add` command.

### Q. Is there any difference between using the https link and the SSH link to clone a repository?
* TODO

### Q. What if you need to use a different name for the download folder rather than the name of the repository with ```git clone```?
* We can add the folder name along with the command like this
```
git clone git@gitlab.com:COHORT_ME_GIT_BASICS_INTERNAL/crio-ME_GIT_BASICS.git MyGitBasicsFolder
```

### Q. Where does `git remote` command get the mapping of remote name & the corresponding links?
* Through the `.git/config` file

### Q. Which command(s) can be used to create a local version of the repository at https://gitlab.crio.do/crio_bytes/me_encapsulation?
`git clone https://gitlab.crio.do/crio_bytes/me_encapsulation.git`

### Q. Which of the following is true regarding the repository you downloaded from Gitlab using the git clone … command?
* Have a folder, `.git`

<hr>

# Milestone #2 - Add new changes
## Saving changes locally
* Create a file, first.txt and add some text to it.
```
$ git status
On branch master
Initial commit
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        first.txt
nothing added to commit but untracked files present (use "git add" to track)
```

* first.txt is an Untracked file.
```
$ git add .
$ git commit -m "Initial commit"
$ git log
commit: 342534325235hfa8e73gf4&*TQGYu3g4r
Author: _______
Date: ______
```

## Let the world know
```
$ git push -u origin master
```

### Q. How would you mark all changes for committing using git add instead of listing out each of the file names?
* `git add -A`
* `git add .`

### Q. How can we move changes to a modified file from the staging area back to the working directory? What if we need to get the file back to the previous committed state?
* We use the `git add` command to move the file from working directory to the staging area. If you try `git status` in that state, Git will tell you to use the `git reset` command to go back.`HEAD` is an alias for the last committed state.
* To remove the changes from working directory as well, use the `git checkout` command.

### Q. Now that we have only a handful of files, it’s easy to remember what changes were newly made. How’d you check the changes made to the local repo since the previous commit?
* The `git diff` command is used to see the difference of file states in Git. By default, `git diff` shows the difference between the working directory and the staging area.
* Use `git diff HEAD` to see changes made since the last commit which is denoted by `HEAD`

### Q. Rename a file and make a commit. Now, make some edits to the file and commit again. `git log --follow <filename>` lists all commits that changed this file. You’ll be able to find commits related to the original file name are also listed out. How does Git detect renames?
* TODO

### Q. What’s the correct sequence of actions for reflecting local changes in the remote repository?
* Make changes to file.txt -> `git add file.txt` -> `git commit` -> `git push` …
* Make changes to file.txt -> `git commit -a` -> `git push` …

### Q. What will the `git add newFile.txt` command do?
* Mark changes made to newFile.txt file for next commit

### Q. Which command makes the local changes visible in the remote Gitlab repository?
* `git push`

<hr>

# Milestone #3 - Being in sync
## Getting updates from the remote
* ` git pull origin master`

### Q. There’s another command, `git fetch ....` How’s it different from a `git pull ...`?
* `git fetch` fetches only metadata related to changes and doesn’t actually make any changes to the project files we have locally. We’ll need to do a separate `git merge` for that whereas `git pull` naively speaking does both 
* `git pull = git fetch + git merge`

### Q. Which of the following is true regarding the `git log` output(when code was pulled after creating the README file via Gitlab)?
* `git pull` added one new commit
* Commit message of the most recent commit is exactly what I entered in the Gitlab UI in Commit Message* *textbox before clicking on the Commit changes button

### Q. Which of the following is true regarding the `git log` output(after resolving the “Updates were rejected because the remote contains work that you do” error)?
* `git pull` added two new commits
* Commit message of the most recent commit is similar to "Merge branch 'master' of ..."

<hr>

# Milestone #4 - Handling merge conflicts
```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
Resolve conflict? (yes/no) yes
```

![Merge Conflict](https://raw.githubusercontent.com/achiv/Notes/main/images/Git_conflict.png)

1. Accept Incoming Change
2. Accept Current Change
3. Remove `<<<<<<HEAD` and `=====` and `>>>>09324832580945` and accept both manually.

<hr> 

# Milestone #5 - Takeaways
## Summary
* Basic workflow in Git: 
  * You modify files in your working directory
  * You stage the files, adding snapshots of them to your staging area (`git add file`)
  * You do a commit, which takes the files as they are in the staging area and stores that snapshot permanently to your local Git repository (`git commit file`)
  * You push the changes from the local repository to the remote repository (`git push`)
  * You pull the changes from the remote repository to the local repository (`git pull`)

![Workflow](https://raw.githubusercontent.com/achiv/Notes/main/images/Git_workflow.png)

* State of the file according to actions

![State](https://raw.githubusercontent.com/achiv/Notes/main/images/Git_state.png)













