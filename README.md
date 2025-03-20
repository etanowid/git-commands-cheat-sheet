# git-commands-cheat-sheet
git commands cheat sheet

# make copy of your branch
`git checkout [your branch]` <br/>
`git checkout -b newbranchname [your branch]`

# stage, commit, push
`git add .` <br>
`git commit -m "bruh"` <br>
`git push origin [your branch]` <br>
<br>
<br>

# squash without rebasing
## commit any working changes on branch "mybranchname", then...
`git checkout master`<br>
`git checkout -b featurebranch`<br>
`git merge --squash tempfeaturebranch`<br>
`git commit -am "squashed commits from featurebranch"`<br>
`git push`<br>
<br>
<br>

# rebase
`git branch` 		// shows all branches <br>
`git checkout dev` <br>
`git pull origin` <br>
`git checkout [your branch]` <br>
`git rebase dev -i` 	# squash all the commits into 1 <br>

// (use reword **r** for the first one, the rest of the commits use **f**) <br>
// change commit message later <br/>

// will open a text file, rename the first one and f for the rest. to cancel `:q!` and run `git rebase --abort` <br>

// if there's merge conflict, go to vscode, resolve it manually, save, click the + (same as running "git add") then go back to terminal and run `git rebase --continue`
<br>

`git rebase --continue` <br>

### once finished, change the commit msg 

`git log | less` 				// shows a more organized commit log ? <br>

`git checkout [your branch]`	<br>
`git push origin [your branch]`		// probably will fail, so run <br>

// same stuff as above <br>
`git checkout dev` <br/>
`git pull origin dev` <br>
`git checkout [your branch]` <br>
`git rebase dev -i` <br>

// normal stuff to commit n push <br>
`git add .` <br/>
`git commit -m 'message'` <br/>
`git push origin [your branch] -f` <br>
<br>
<br>

# rebase to remove specific commit
In the scenario that I want to remove a commit on a weekly release deployment branch <br>
`git checkout gke`<br>
`git pull`<br>
`git checkout [existing-branch-2024-12-17]` # this is the branch that has the commit to be removed. now has 3 commits.<br>
`git log -4` # copy the most bottom commit hash, this will give you all current branch's commits prior to this hash<br>
`git rebase -i [commit-hash]` # will open the rebase editor, delete the entire line of the commit to remove, then save.<br>
`git push -f --set-upstream origin [existing-branch-2024-12-17]`<br>
Check the PR, it will now have 2 commits only
<br>
<br>


# to rollback to previous commit
`git log | less`		// will show shorter log, copy the hash for the commit you WANT <br/>
`git reset --hard [commit hash]` <br>
`git log` 		// to check, should have latest commit = hash commit <br>
<br>
<br>

# to cancel previous push
`git reset --hard HEAD@{1}`		// will move head to previous commit, then push<br/>
`git push -f` <br>
<br>
<br>

# to cancel git commit --amend
if accidentally committing to the previous commit but need to keep the 2 commits separate<br>
https://stackoverflow.com/questions/1459150/how-to-undo-git-commit-amend-done-instead-of-git-commit<br>
`git reset --soft HEAD@{1}`
<br>
<br>

# rebase the last 3 commits 
`git rebase -i HEAD~3` 	 <br>
// pick, squash, squash <br>
`git push -f` <br>

# to fetch latest commit (if theres new changes from someone else on your branch)
`git fetch` <br>
`git merge` <br>


# will update to the latest commit, change commit msg
`git add .` <br>
`git commit . --amend` 	 <br>
`git push origin [your branch] -f` <br>
<br>
<br>

# create copy of a repository on my own repository
Don't initialize it with a README, .gitignore, or license. <br>
<br>
Clone the other repository to your local machine. <br>
`git clone https://github.com/other-account/other-repository.git` 
<br>
<br>
Rename the local repository's current 'origin' to 'upstream'.<br>
`git remote rename origin upstream` 
<br>
<br>
Give the local repository an 'origin' that points to your repository.<br>
`git remote add origin https://github.com/my-account/my-repository.git`
<br>
<br>
Push the local repository to your repository on github. <br>
`git push origin master`
<br>
<br>

# get the remote branch in local. creates local branch which tracks remote branch
`git fetch` (pull all branches to local)<br>
`git branch --track <branchNameonGithub> <origin/localbranch>`
<br>
<br>

# want to move local changes from dev to subtask branch
`git fetch`<br>
`git stash` (saves changes in vscode locally) <br>
`git checkout -b subtask/blah/blah` <br>
`git stash apply` (put the saved changes in the new subtask branch) <br>
<br>
<br>

# want to stash local changes and pull from another branch
`git stash` (saves changes in current branch locally) <br>
`git checkout [whatever branch]` <br>
`git pull` <br>
`git stash pop` (in subtask branch, put the stashed changes in current branch im on) <br>
<br>
<br>

# simple stash and pop
`git stash` (saves changes in current branch locally) <br>
`git checkout [whatever branch]` <br>
`git stash pop` (in subtask branch, put the stashed changes in current branch im on) <br>
can do `git stash list` and pop using index `git stash pop 1`
<br>
<br>

# change naming
Rename your local branch: <br>
If you are on the branch you want to rename: <br>
`git branch -m [new name]` <br>
If you are on a different branch: <br>
`git branch -m [old name] [new name]` <br>
Delete the old-name remote branch and push the new-name local branch: <br>
`git push origin :[old name] [new name]` <br>
Reset the upstream branch for the new-name local branch: <br>
Switch to the branch and then: <br>
`git push origin -u [new name]`
<br>
<br>

# revert changes not committed
`git checkout -- .` <br>
<br>
<br>

# cherry-pick
// added commits and pushed on branch A <br>
`git checkout master`<br>
`git checkout -b 'new branch B'`<br>
`git cherry-pick <commit hash from any branch u want in this case, A>` <br>
// new branch B will have the commits on branch A <br>
// if need multiple commits from branch A <br>
`git cherry-pick <next commit hash from branch A>` <br>
`git commit -m 'message'`<br>
`git push`<br>
<br>
<br>

# force local checkpoint to point to remote checkpoint
`git reset --hard origin/checkpoint`
<br>
<br>

# reset where HEAD points
`git reset --hard HEAD^` // head points to 1 previous commit on checkpoint. throw away all uncommitted changes, reset everything to previous commit <br>
`git reset --hard HEAD^^` // head points to 2 previous commit on checkpoint <br>
same with
`git reset --hard HEAD~1` <br>
<br>
<br>

# cancel the previous commit (uncommit), but leave everything else intact
`git reset --soft HEAD~1` <br>
# uncommit and unstaged
`git reset HEAD^` <br>


# if someone push a change to remote, and u want to fetch
`git fetch origin person1/zstd-compress` <br>
`git checkout person1/zstd-compress` <br>
`git reset head~1` // Shows Unstaged changes after reset <br>
`git checkout master`<br>
`git checkout -b me/zstd-compression` <br>
`git add .` <br>
`git commit -m 'init'` <br>
`git push`<br>
<br>
<br>

# creating new branch off of checkpoint
`git checkout checkpoint` <br>
`git pull` <br>
`git checkout -b [new branch name]` <br> 
`git commit` <br>
`git push` <br>
<br>
<br>

# if want to pull someone else’s feature branch 
can start on master branch
`git fetch origin edriana-branch:edriana-branch` <br>
`git checkout edriana-branch`
# If you want to continue working after they pushed 
`git pull origin edriana-branch`
<br>
<br>
<br>

# cherry-pick branch for late branch promo
`git add .` <br>
`git fetch origin 12.90-phantom:12.90-phantom` <br>
`git checkout 12.90-phantom` <br>
`git cherry-pick [your change]` <br>
`git checkout -b [your new branch]` <br>
<br>
<br>

# Merge the Latest Master Branch into a Local Branch
Occasionally, a change can occur in the master branch that you'd like to incorporate into your local branch. can merge the remote master branch directly into your local branch <br>

`git status` to confirm you're own your local branch <br>
`git pull origin master` <br>
Unlike other pulls, this command is actually pulling in the master branch, merging it with your branch, and then committing that change to your local branch - a commit message will be auto-generated when you run the command. <br>
To accept the commit message (which will appear in a Terminal text editor), type :wq and then Return to save and quit the text editor.
<br>
<br>

# Reset the Local Master Branch
If you accidentally commit changes to the master branch, can reset your master branch as follows <br>

`git status` to ensure you're on the master branch <br>
`git fetch origin` <br>
`git reset --hard origin/master` <br>
<br>
<br>

# Revert a cooled PR
If you cool a change that you'd later like to revert, can revert your changes <br>

`git checkout master` <br>
`git pull` to ensure you have the latest master branch <br>
`git checkout -b "new_branch_name"` <br>
`git revert <sha1 hash>` where sha1 hash is the 7-character alphanumeric code next to the very last commit in your original PR prior to the bot closed this comment (it will look something like "64d4b93") <br>
`git push` and then open a new PR, which will contain changes to undo your original PR. <br>
<br>
<br>

# Revert Changes/Commits for a Single File from a Branch
In circumstances where you would like to revert a single file (e.g., there's a merge conflict with the master branch and you'd like to merge in the entire new file and then re-add your changes; you change your mind about a single file and replacing via copy-paste from an older version seems risky), follow these steps: <br>

`git log path/to/file` <br>
This will display the log of commit changes to the file in question; find the commit hash for a prior commit that contains the version of the file you would like to revert to (typically the commit just prior to your first commit in your current branch) - the hash will be displayed in yellow font. <br>
`git checkout <commit hash> path/to/file` <br>
`git commit -m "<message>"` <br>
<br>
<br>
