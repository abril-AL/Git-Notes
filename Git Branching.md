
- Definition - diverge from the main line of development and continue to do work without messing with that main line
- most VCS have a form of branching, and expensive, usually requires making a copy, as a result - less merging
- Gits branching is special, very lightweight, nearly instantaneous, switching between branches just as fast, encourages merging often bc it can handle it

## Branching in a nutshell
- when you commit, git stores a pointer to the snapshot of the content you staged, object has other info aswell ( name email etc )
- a branch is essentially a lightweight movable pointer to one of these commits
- creating a new branch - creates a new pointer to move around
- current branch is called `HEAD`
- `git branch` creates new branch - doesnt switch to it
- switching branches - `git checkout <branchname>`

## Basic Branching and merging
- motivation: say theres an issue, want to fix it, switch to a production branch, 
- `-b ` option , switch to a new branch
- curren branch can move ahead of master, can work on fixing the issue here instead of main part, can deploy fix later or go back to original
- to go back to master: `git checkout master`
- can have multiple branches at once
- git wont let you branch without a clean working directory or uncommitted staging area that conflits with branch youre checking out
- when you switch branches, Git resets your working directory to look like it did the last time you committed on that branch
- merging: `git merge <branch_choice>` ( most likely want to switch to master first )

## Basic Merging
- if merging isnt from a direct ancestor branches, git does a 3 way merge with common encestor, and two branches, creates a new snapshot
	- ![[mergeimg.png]]
	- keeps old brank open,  can delete it if you want
- Basic Merge Conflicts
	- Wont always merge smoothly
	- ex. if u change 2 different files differenly in two branches, git cant merge them clearly
	- have to either choose one or merge the content yourself
	- `git status` will show `both modified: ` , remain unmerged, staging them after an edit marks it as resolved
	- graphical tool: `git mergetool` , visual merge tool to walk through conflicts
		- after you exit, git asks if you resolved it, and stages the files
		- useful to add comment on how you fixed the merge

## Branch Management
- `git branch`
	- no arguments, it lists the current branches
	- `*` indicates the branch you currently have checked out
- `git branch --merged` or `--no-merged`
	- filter branches that have/havent been merged
	- defaults to what is merged to current branch, can also speficy a commit/branch name
- `git branch -d <branch_name>` - delete a branch
	- cant delete non merged branches, unless u force it with `-D`
- Changing a branch name
	- want to change name but keep history, and branch name on remote
	- Rename locally - `git branch --move bad-name correct-name`
	- Rename to others/remote - `git push --set-upstream origin correct-name` , then you need to delete old name still present on remote with `git push origin --delete bad-name`
- Changing the master branch name
	- `git branch --move master main` , rename master to main
	- let others see with `git push --set-upstream origin main`
	- need to then fix anything that would rely on the old cnfiguration
	- then canfinally delete old name on remote with `git push origin --delete master`

## Branching Workflows
- what to do with branching, common workflows
- Long-Running Branches
	- because of simple 3 way merge, we can have multiple long running branches that merge can merge regularly
	- can have braches marking different points of stability
- Topic branches
	- short lived branches created for single feature/work
- rember all this is local, remote doesnt know...

## Remote Branches
- one way: `git ls-remote <remote>`, or `git remote show <remote>` for remote branches as well as more information
- Another way: remote tracking
	- references to state of remote branches 
	- local references: you can't move, only git moves then whenever it does network communication
	- to synchronize: `git fetch <remote>` grabs any data you don't have yet and moves remote reference to up-to-date position 
	- can fetch from other remotes as well
- Pushing
	- `git push <remote> <branch>`
- Tracking Branches
	- looking at a local branch from a remote-tracking branch creates a "tracking branch"
	- Def: local branches that have a direct relationship to a remote branch, ex if you pull while on a tracking branch, git automatically knows what server to fetch from and what branch to merge in
	- cloning generally creates master branch that tracks `origin/master` 
	- `git checkout -b <branch> <remote>/<branch>`
	- Git shorthand `git checkout --track ` 
	- set up upstream: `git branch -u origin/<branch>` (?)
- Pulling
	- fetch will fetch changes, but won't modify working directory, have to merge it yourself
	- `git pull` is a combination of fetch and merge in one cmd
- Deleting Remote Branches
	- if you're done with a remote branch, can delete with `git push origin --delete <remote-branch>`
	- removes pointer from the server, keeps data there for a bit in case it was accidental

## Rebasing
- two main ways to integrate changes between branches: `merge` and `rebase`
- The basic rebase
	- `git rebase <branch>`
	- take all the changes that were committed on one branch and replay them on a different branch 
	- goes to the common ancestor, gets the difference and saves to a temp file, resets current branch to same commit as the branch we're rebasing to, and applying each change in turn
	- makes for a clearer history, more linear
- Perils of rebasing
	- drawback, do not rebase commits that exist outside your repository and that people may have based work on
	- rebasing abandons existing commits and creates new ones that are similar but different
		- if u push and others pull that rebased repo, collaborators will have to re-merge and it gets messy when you then have to pull their pushes
- Rebase vs Merge
	- depends on what you want your commits to be/represent: a record of what actually happened or a story of how the project was made, for story: use tools like `rebase` and `filter-branch`
