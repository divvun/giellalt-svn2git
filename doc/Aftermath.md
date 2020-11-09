# Aftermath

To be fleshed out, but the following points are at least relevant:

* transfer bugzilla issues to github issues (only open ones, or old ones too?)
    * see [this project](https://github.com/orgs/giellalt/projects/4)
* set up branches according to git-flow and our needs
	* partially DONE, to be further evaluated
* set up CI for the various integration branches
	* partially DONE, ongoing work
* make sure everything is working also for svn users
	* DONE (at least svn ignore, everything else works as before)
* define production languages - see below on maturity
* transfer dictionaries to github - repo prefix `dict-`
* possibly transfer other stuff to github:
	* tools
	* techdoc (`site-giellalt`?)
	* the other sites, repo prefix `site-`?
	* make the site build and publish on push/commit using github actions

# Language model maturity classification

We need to clearly communicate the maturity of a language code base. For this we could have four categories as follows (+ unknown/undefined):

1. Production - colour: green
1. Beta - colour: yellow
1. Alpha - colour: red
1. Experiment / student exercise - colour: black

These should be used as labels in the README for each language, and also in the [registry](https://github.com/divvun/registry). The labels should look as follows:

* ![Maturity: Production](https://img.shields.io/badge/Maturity-Production-brightgreen.svg)
* ![Maturity: Production](https://img.shields.io/badge/Maturity-Beta-yellow.svg)
* ![Maturity: Production](https://img.shields.io/badge/Maturity-Alpha-red.svg)
* ![Maturity: Production](https://img.shields.io/badge/Maturity-Experiment-black.svg)
* ![Maturity: Production](https://img.shields.io/badge/Maturity-Undefined-lightgrey.svg)

The criterias for the various levels are, in reverse order (obviously some of these do not apply to keyboards):

## Experiment ![Maturity: Production](https://img.shields.io/badge/Maturity-Experiment-black.svg)

This category also covers student exercises (published with permission). The point of such exercises is not to make a working system, but to explore the possibilities for language technology. Such work can of course be extended and in the end result in a fully working, production tool.

* fragmentary grammar/model/layout
* less than 1k lexical entries
* only available by building locally, may not build at all

## Alpha ![Maturity: Production](https://img.shields.io/badge/Maturity-Alpha-red.svg)

* grammar/model/layout mostly complete
* lexicon between 1k and 10k entries
* only available for internal testing
* rule of thumb: it can be built locally and used for something

## Beta ![Maturity: Production](https://img.shields.io/badge/Maturity-Beta-yellow.svg)

* grammar/model/layout complete
* lexicon has more than 10k entries
* running text coverage above 80 %
* CI/CD working for the tools being provided, entries in Divvun Manager with delivery to the nightly channel
* rule of thumb: it can easily get from the nightly channel/Dev app/etc - it must be testable by the user community

## Production ![Maturity: Production](https://img.shields.io/badge/Maturity-Production-rightgreen.svg)

* grammar/model/layout complete
* lexicon has more than 30k entries (but subject to realworld realities & limits)
* running text coverage above 90 %
* at least one contact person in the language community that is willing to or being payed to be a first line support person and language resource maintainer
* CI/CD working for the tools being provided, entries in Divvun Manager, documentation, etc, with delivery to the stable channel
* Release `1.0.0` or higher of either speller or analyser/`giella-XXX` package
* rule of thumb: it is available in the stable channel/default App/etc
