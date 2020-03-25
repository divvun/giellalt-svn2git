# Users, groups and administrators

[dadmin](https://github.com/divvun/project-dadmin) can be used to both clone a set of repos, as well as add users and groups.

Direct commit access policy is not yet defined, feedback and viewpoints are very welcome.

What is very likely is that there will be a policy containing at least the following points (git-flow like):

* no direct commits on `master` (it will be a protected branch)
* default commit branch should be `develop`
* it would be beneficial if svn users could commit to their own branch
	* branches are fully supported by the git-svn bridge
	* how to enforce this on users is another story...
* CI on every commit on `develop`/`svn-develop`, but only with the default config, to reduce build and test time