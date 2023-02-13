## Revision selection
- can refer to a single commit, many ways to refer to them
	- Short SHA-1, hash, at least 4 chars and unambiguous
	- Branch References - use branch name if it's the commit at the tip of the branch
	- RefLog Shortnames - git logs where your HEAD and branch references have been for past few months, can view reflog with `git reflog` 
	- Ancestry References - `^` at the end of a reference will tell git they mean the parent of that commit
- commit ranges
	- Double dot - asks git to resolve a range of commits reachable from one commit but not another
		- `git log master..<other-branch>`
		- the opposite `git log <other-branch>..master`
	- multiple points
		- what if you want to specify multiple branches, such as seeing what commits are in any of several branches that aren’t in the branch you’re currently on
		- can use `^` or `--not` 
		- `git log refA..refB`    `git log ^refA refB`    `git log refB --not refA`
	- Triple dot
		- specifies all the commits that are reachable by _either_ of two references but not by both of them, like XOR(?)
		- `git log --left-right master...experiment`

## Searching
- what if you need to find where a certain function is called or defined in database
- git lets us look through code and commits

- Git Grep
	- `git grep <options> <grep-exp>`
	- `-n` or `--line-numer` prints line numbers where git found matches
	- `-c` or`--count` prints amount of times it was found in each file
	- `-p` or `--show-function` displays enclosing method/function for each match
	- can also search for complex combinations with `--add` - ensures multiple matches must occur in same line of text
- Git Log Searching
	- want to know *when* something existed or was originally introduced
	- use the `-S` option, shows the commit, also has a `-G` option
- Line Log searching
	- run git log with `-L` and it will show you the history of a function or line of code in your codebase

## Debugging
- File annotation
	- if u find a bug and want to track down when/where it was introduced and why, use file notation
	- `git blame <file>`
		- can further specify line number
		- will list which committer is responsible and a SHA1
		- git can implicitly record filename changes
		- `-C` option will try to figure out is code was pasted from other file
- Binary Search
	- what if you don't know what the issue is
	- `git bisect` does a binary search through the commit history to help find which commit introduced an issue
	- `git start`   `git run <sh>`  `git bad`   `git good <last-good-version>`   `git reset `