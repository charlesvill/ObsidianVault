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
