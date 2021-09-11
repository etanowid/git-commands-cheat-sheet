# git-commands-cheat-sheet
git commands cheat sheet

# make copy of your branch
git checkout [your branch]
git checkout -b newbranchname [your branch]


git branch 		# shows all branches
git checkout dev
git pull origin
git checkout [your branch]
git rebase dev -i 	# squash all the commits into 1

# (use reword "r" for the first one, the rest of the commits use "f")
# change commit message later

# will open a text file, rename the first one and f for the rest. to cancel ":q!" and run "git rebase --abort"

# if there's merge conflict, go to vscode, resolve it manually, save, click the + (same as running "git add") then go back to terminal and run "git rebase --continue"


git rebase --continue

# once finished, change the commit msg 


git log | less 				# shows a more organized commit log ?

git checkout [your branch]	
git push origin [your branch]		# probably will fail, so run
git push origin [your branch] -f
==========================================================================
# same stuff as above
git checkout dev
git pull origin dev
git checkout [your branch]
git rebase dev -i
git push origin [your branch] -f
==========================================================================
# normal stuff to commit n push
git add . 	# might be unnecessary?
git commit -m 'message'
git push origin [your branch] -f
==========================================================================
# to rollback to previous commit
git log | less		# will show shorter log, copy the hash for the commit you WANT
git reset --hard [commit hash]
git log 		# to check, should have latest commit = hash commit
==========================================================================
# cancel the previous commit 
git reset --soft HEAD~1
==========================================================================
git rebase -i HEAD~3 	# rebase the last 3 commits
# pick, squash, squash
git push -f
==========================================================================
# to fetch latest commit (if theres new changes from someone else on your branch)
git fetch
git merge
==========================================================================
# will update to the latest commit, change commit msg
git add .
git commit . --amend 	
