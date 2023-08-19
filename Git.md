**commit** commits changes

**branch** creates a branch (controls branches)
	-f forces a branch to the specified commit 
```bash
git branch -f main HEAD~3 #moves the branch to the HEAD~3
```
**checkout** switches an active branch (controls HEAD)
	-b creates a branch to switch to
	-branch^ moves HEAD one commit behind
	-brach~5 moves HEAD several commits behind
```bash
git checkout main~2 #moves HEAD 2 commits ealier in main
```
**merge** merges branches
```bash
git checkout main #changes to bugFix branch
git merge bugFix #merges the specified branch with the current one
```
**rebase** moves the last commit of a branch in the end of the specified branch. A different way to merge branches. To merge after rebasing switch to the branch and rebase it as well.
	-i interactivly choose commits to rebase
```
git rebase -i HEAD~5
```

**reset** moves the branch back, forgetting (?) the commits that were left behind. Used for local branches because you dont need to multiply commits
```bash
git reset main~5
```
**revert** creates a new commit that reverts all the changes made. Used for remote branch because everyone needs to have the exact same commit history.
```bash
git revert HEAD~2
```
**cherry-pick** chooses specific commits to add to the branch

**clone** copies a remote repository to a local machine

**fetch** synchronizes the remote repository on a local machine. Doesn't alter the data on a local machine

**pull** fetches and merges
	--rebase 

**push** sends changes to a remote repository

git check-ignore