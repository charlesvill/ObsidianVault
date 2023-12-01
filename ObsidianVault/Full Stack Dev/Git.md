#### Deeper look at git (TOP)
- topcis to cover: 
	- History-changing Git commands
	- different ways of changing history
	- Using remotes to change history
	- Hangers of higtory-changing operations
	- Pointers

##### Changing History
- topics needed to know: changing most recent commits, changing multiple commit messges and reordering commits, squashing commits together and splitting up commits. 
- What does `git commit --amend` do? 
	- allows you to rewrite the previous commit that has not been pushed to the repo yet!
- what does `git rebase` do? 
	- allows you to rewrite commits from previous that were not necessarily the most recent commits
	- `git rebase -i HEAD~2`  this will allow you to fix a commit two commits ago
	- change the tag `pick` to `edit`. save, then close. 
	- `git commit --amend` 
	- then make the changes and save. run `git log` to make sure that it got fixed. 
##### Squashing Commits 
- taking two previous commmits and combining them into one commit
- how to?
	- Start with `git rebase -i --root` (or the commit that the other will merge into)
	- change the commit you want to squash from `pick` to `squash` 
	- hit `git commit --amend` where you'll be able to rename it and hit save, you're done. 
##### splitting up a commit
- if a commit has too much and you want to split it up into smaller commits, you can: 
	- run `git rebase -i <commit>` 
	- change `pick` to `edit` on the commit you want to split up
	- run `git reset HEAD^` ( resets the commit to the one right before HEAD)
	- then run `git add test3.md && git commit -m 'Create 3rd file'` and the same for the other commit you're splitting
	- *important to note that reset willl overwrite the staging area with whatever was right before HEAD before you hit the reset button, so make sure you know  why you're using this command*
	- you can also use `git reset --soft` which will point to the previous commit without changing the staging area data. 
##### Branches are pointers 
- in reality when we say a commit of a branch is a snapshot, what it means is its a copy of your project and all a branch is, is a pointer to one specific commit. we have access to thte other commits because that one commit also has a reference or pointer to the previous commit as well.
**more resources on git rebasing and reset: 
rebase: https://git-scm.com/book/en/v2/Git-Branching-Rebasing
reset: https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified**
