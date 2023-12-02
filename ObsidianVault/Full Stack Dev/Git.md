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

#### working with remote repositories


##### when your local repo is behind the online repository
- if you try to push it will reject because the version of the repo online is ahead compared to your local one. one answer `git push --force` this however should be avoided because if you're workign with other people, it will erase the worth of others
	- the alterantive: `git fetch`, `git merge` then attempt to push again. this updates your local and then you can push your updates..
- What happens if you made a mistake in the last commit that you pushed?
		- you can hit it with the git revert HEAD which will allow you to edit your last commit, then y ou will save the changes and then push to the repo which will apply the fixes to the online repo
##### review of the most dangerous commands
- `amend` `rebase` `reset` `push --force` are the especiallly dangerous when working with others
- Best practices: 
	- try only using on branches you're working on by yourself
	- dont push after every commit, changing published history should be avoided
	- never amend commits that have been pushed to remote repo
	- never rebase  repo that others may work on
	- never reset commits that have been pushed to remote repo
	- use push force when appropriate and preferably default to git push --force-with-lease
- *when you have merge conflicts: * https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts
- *thinking like git: * https://think-like-a-git.net/

- what is a way that you could visualize your git history at the same time?
	- run the line `git log --oneline --abbrev-commit --all`
- good practice with rebase and merge: 
	- create a branch. its like saving your game before you battle the boss
	- *come back to the think like a git @ testing out merges to get more comfortable with merges*

#### Git in the real world
- go back to the lesson git in the real world TOP when getting in trouble with git

##### git workflow for open source contributions
- the key players: 
	- the `upstream` original gh repo
	- the `origin` your fork of the repo