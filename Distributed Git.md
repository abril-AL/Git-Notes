## Distributed Workflows
- every developer is potentially a hub or node, can contribute to other repos and maintain public repos others can base work off of, lots of possibilities

- Centralized Workflow
	- single collaboration model
	- one central hub ( or repository ) accepts code and everyone synchronizes with it

- Integration-Manager Workflow
	- possible to have a workflow where each dev has write access to a public repo and read access to everyone else's
	- 1 "official" repo, public clones with own pushes will send a request to official to push in their changes 

- Dictator and Lieutenants Workflow
	- used mostly for repositories with large amount of contributors
	- integration managers called lieutenants manage different parts of the repository
	- lieutenants have one integration manager called the dictator that will push their work to a reference repo where all other collaborators will pull from

- many different patterns possible

## Contributing to a Project
i skimmed this section
- Variables
	- active contributor count - how many ppl actively contributing code and how often
	- workflow - is it centralized ? Integration managers ? Peer-review ? 
	- Commit access - how does the project accept contributions ?
- Commit guidelines
	- leave good messages, no whitespace errors
	- commits should be logically separate, often enough
	- make it easy to pull/revert changes
- private small team
	- small amt of devs working on closed source project, other devs have push access
- private managed team 
	- small groups collaborate on small features, integrated by another party
- Public project over email
	- email edit patches to other devs
	- `git send-email *.patch`

## Maintaining a Project
- Working in topic branches
	- temporary branch to try something out
- applying patches from email
	- `git apply /tmp/location`
	- like running `patch p1`
	- can also use `git apply --check` to see if a patch  applies cleanly
- Applying a Patch with `am`
	- if contributor used `format-patch` to generate their patch, only have to use `git apply` for legacy patches
- checking out remote branches
	- add the remote, can later add patches
- determining what is introduced
	- check what's different from master in the topic with `git log contrib --not master`
- integrating contributed work
	- Merging Workflows
		- merge with the master
		- can be problematic if dealing with large project
		- might want to use a two phase merge cycle
	- Large merging workflows
		- safe things merged into `next`
		- topics that still need work go to `seen`
		- when they're ready, they are merged to master
		- `next` and `seen` rebuilt from master, `master` moves forward
- Rerere
	- if you're doing lots of merge/rebasing rerere feature can help
	- stands for "reuse recorded resolution"
	- way of shortcutting manual conflict resolution
	- looks at past conflict fixes and tries to apply something similar
- tagging your releases 
	- ?
- Generating a Build number
	- `git describe master` git generates a string of the name of the most recent tag earlier in that commit followed by number of commits since that tag followed by partial SHA-1
- Preparing a release
	- to release a build, will want to first create an archive of the latest snapshot of your code for non-git users `git archive`
	- creates tarball with latest snapshot under the `project` directory
- The Shortlog
	- quick way to summarize commits in a given range
	- ex for a summary of all the commits since your last release, if your last release was named v1.0.1: `$ git shortlog --no-merges master --not v1.0.1