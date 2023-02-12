# About Version Control 
- local VC - save a copy in perhaps another directory, but we dont want to save copies, error prone
- Centralized VS - want to collaborate with others, single server, downside is if server is down, no one can work on project 
- Distributed VS - clients mirror the repository rather than check out latest snapshot
	- client repositories can be copied back to be restored if at any point the servers go down, every clone is a full backup
	- deal well with having several remote repositories for collaboration
	- several workflows possible with centralized systems

# What is git ?
- Snapshots 
	- main difference from other VCS
	- Other VCS store information as a list of file-based changes
	- git thinks of data as a series of snapshots, like a picture of what the files look like 
	- doesnt store unchanged files, just a link to previous identical file
	- Git is a **stream of snapshots**
	- ![[git-snapshots.png]]
- Operations are local
	- doesnt need info from other pc or network
	- fast - have access to history of project locally
	- other CVS might require network connection
- integrity
	- eerything is checksummed
	- cant change anything without git knowing
- Generally only adds data
	- hard to do "undoable" things or erase data
	- data after a commit is difficult to lose
	- So, we can experiment without anger of breaking everything
- Three States
	1) `modified` - you changed the file, but havent committed it to the database yet
	2) `staging` - you have marked a modified file to go into the next commit snapshot
	3) `committed` - the data is safely stored in local database
	- main sections of a git project are therfore: the working tree, the staging area, and the git directory
	- ![[git-stages.png]]


## The Command Line
- way to use git is through command line
- only place you can run **all** git commands

## Installing ( windows )
- git website
- https://git-scm.com/download/win
- `git config --list`
	- lists config details like name, email, remote origin, etc

## Getting Help
- `git help <verb>` 
- `man git-<verb>`
- help is accessible offline
- help option fo git commands as well `-h`