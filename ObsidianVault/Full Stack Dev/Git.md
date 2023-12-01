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