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

## once finished, change the commit msg 

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

# to rollback to previous commit
`git log | less`		// will show shorter log, copy the hash for the commit you WANT <br/>
`git reset --hard [commit hash]` <br>
`git log` 		// to check, should have latest commit = hash commit <br>

# cancel the previous commit 
`git reset --soft HEAD~1` <br>

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
// added commits and pushed on branch A
`git checkout master`
`git checkout -b 'new branch B'`
`git cherry-pick <commit hash from any branch u want in this case, A>`
// new branch B will have the commits on branch A
// if need multiple commits from branch A 
`git cherry-pick <next commit hash from branch A>`
`git commit -m 'message'`
`git push`

# force local checkpoint to point to remote checkpoint
`git reset --hard origin/checkpoint`
<br>
<br>

# reset where HEAD points
`git reset --hard HEAD^` // head points to 1 previous commit on checkpoint <br>
`git reset --hard HEAD^^` // head points to 2 previous commit on checkpoint <br>
same with
`git reset --hard HEAD~1` <br>
<br>
<br>


# uncommit, but leave everything else intact
`git reset --soft HEAD^` <br>
# uncommit and unstaged
`git reset HEAD^` <br>
# throw away all uncommitted changes, reset everything to previous commit
`git reset --hard HEAD^` <br>
<br>
<br>


# creating new branch off of checkpoint
`git checkout checkpoint` <br>
`git pull` <br>
`git checkout -b [new branch name]` <br> 
`git commit` <br>
`git push` <br>
