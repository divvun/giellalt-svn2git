# The actual move

See [this page](https://giellalt.uit.no/infra/InfraUpgradeAndGithub.html#Procedure+for+moving), which links to [this page](https://github.com/subethaedit/UniversalDetector).

* [svn2git](https://github.com/nirvdrum/svn2git)
* [Migrating to Git](https://git-scm.com/book/be/v2/Git-and-Other-Systems-Migrating-to-Git)
* [Migrating From SVN to Git](https://gist.github.com/barrysteyn/2ba947313e0a4ad086c3)
* [SVN to Github migration](https://stackoverflow.com/questions/50106970/svn-to-github-migration)

Basically, it boils down to the following:

* get list of svn committers, with their github username and email
* clone each language dir locally from svn using git-svn
	* should be a loop, ie clone all at once, but creating a repo for each language
	* skip whatever we say we want to skip
* do some cleanup where needed (ie throw away test commits by users never seen again, large binary files we don't want in git, etc)
* 