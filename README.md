# git-commands-cheat-sheet
git commands cheat sheet

# make copy of your branch
`git checkout [your branch]` <br/>
`git checkout -b newbranchname [your branch]`

# rebase
`git branch` 		// shows all branches <br/>
`git checkout dev` <br/>
`git pull origin` <br/>
`git checkout [your branch]` <br/>
`git rebase dev -i` 	# squash all the commits into 1 <br/>

// (use reword "r" for the first one, the rest of the commits use "f") <br/>
// change commit message later <br/>

// will open a text file, rename the first one and f for the rest. to cancel ":q!" and run "git rebase --abort" <br/>

// if there's merge conflict, go to vscode, resolve it manually, save, click the + (same as running "git add") then go back to terminal and run "git rebase --continue"
<br/>

`git rebase --continue` <br/>

# once finished, change the commit msg 

`git log | less` 				// shows a more organized commit log ? <br/>

`git checkout [your branch]`	<br/>
`git push origin [your branch]`		// probably will fail, so run <br/>

// same stuff as above <br/>
`git checkout dev` <br/>
`git pull origin dev` <br/>
`git checkout [your branch]` <br/>
`git rebase dev -i` <br/>

// normal stuff to commit n push <br/>
`git add .` <br/>
`git commit -m 'message'` <br/>
`git push origin [your branch] -f` <br/>

# to rollback to previous commit
`git log | less`		// will show shorter log, copy the hash for the commit you WANT <br/>
`git reset --hard [commit hash]` <br/>
`git log` 		// to check, should have latest commit = hash commit <br/>

# cancel the previous commit 
`git reset --soft HEAD~1` <br/>

# rebase the last 3 commits 
`git rebase -i HEAD~3` 	 <br/>
// pick, squash, squash <br/>
`git push -f` <br/>

# to fetch latest commit (if theres new changes from someone else on your branch)
`git fetch` <br/>
`git merge` <br/>


# will update to the latest commit, change commit msg
`git add .` <br/>
`git commit . --amend` 	 <br/>
<br>
<br>

# Create a new repository at github.com. (my own repository)
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
