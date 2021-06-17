# Aftermath

To be fleshed out, but the following points are at least relevant:

* transfer bugzilla issues to github issues (only open ones, or old ones too?)
    * see [this project](https://github.com/orgs/giellalt/projects/4)
* transfer more to github:
    - dictionaries - repo prefix `dict-`
    - tools/
    - techdoc/
    - priv/
    - art/
    - corpora - repo prefix `corpus-`
    - …
* possibly transfer other stuff to github:
    * tools
    * techdoc (`site-giellalt`?)
    * the other sites, repo prefix `site-`?
    * make the site build and publish on push/commit using github actions

After moving stuff to github, there might be a need to clean and remove files from the history.
For that the [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) is a great tool.

## DONE tasks

* set up branches according to git-flow and our needs
    * partially DONE, to be further evaluated
* set up CI for the various integration branches
    * partially DONE, ongoing work
* make sure everything is working also for svn users
    * DONE (at least svn ignore, everything else works as before)
* define production languages - DONE
