# External build rules

To enforce true language independence for the core build rules, they should be moved out of each language dir (`am-shared/`) to `giella-core/am-shared`. There is also a separate repo (`giella-shared`) of shared language resources (language data such as digits, names or acronyms, or shared filter regexes), these should be treated the same way wrt building. To make automatic builds work from source check-out or clone, there are a number of things to consider.

# Problem

`am-shared` is needed at `autoreconf` time, which requires that all build resources are available at a known and relatively local position. This makes sharing the resources among languages more tricky, since every language is its own repository in GitHub. Thus these resources are not automatically available by just checking out the language repo, which means that the language tools can not be built.

Using environment variables is not ideal, since we would have to rely on them all the time, for all builds (given that the resources must be available for `autoreconf`).

# Basic idea

> `giella-shared` & `giella-core` as git submodules or subtrees in each language. This can be overriden by `autogen.sh` for each language, see below.

Both resources should available in a dir `deps/` in each language, so that the path to the build resources will always be: `$(top_srcdir)/deps/giella-core/am-shared/*`, and similar for `giella-shared`.

## Submodule vs subtree

Most operations seem easier using `git subtree`. The main issue for the GiellaLT use cases seems to be that with `git subtree` the subtree is always included, for all users. That does not go well for users working with many languages at the same time, where the desired behavior is that the subproject code is *NOT* cloned, but instead cloned as an entirely separate repo parallel to all languages. In this case the place of the submodule should be a symbolic link to the independent repo.

`git submodule` on the other hand seems to allow this by opting *NOT* to clone submodules. This leaves the `deps/` subdir open for setting up symlinks instead.

If the regular user is by default not cloning submodules, and instead relying on `./autogen.sh`, we can get the desired behavior for all users: they can cd into the `giella-shared` dir, make changes and commit + push (since it is a completely independent repo). And for CI and other build systems it is easy to enforce cloning of submodules, so that these read-only usages get all the code in one go.

# Usage scenarios

## One language

### Cloning using git

If cloned with submodules, everything will be in place, and nothing more needs to be done.

If cloned without submodules, running `./autogen.sh` will clone the required resources and make them available in the correct place.

If we're using `git subtree` instead, everything will also be in place, and nothing more needs to be done.

| Submodule           | Subtree                                            |
| ------------------- | -------------------------------------------------- |
| off by default      | always included                                    |
| allows independent clone using `./autogen.sh` | won't work with `./autogen.sh` |
| hard to commit/push | commits are transparent                            |
| update separately   | updates automatically                              |

### Checking out using svn

The `svn` interface of GitHub does not give access to submodules. Instead the resources will be checked out by `./autogen.sh` and made available in the correct place.

| Submodule           | Subtree                                            |
| ------------------- | -------------------------------------------------- |
| does not work       | works transparently                                |
| requires `./autogen.sh` | won't work with `./autogen.sh`                 |
| hard to commit/push | commits are transparent                            |
| update separately   | updates automatically                              |

## Multiple languages

If many languages are cloned or checked out in parallel (and without the submodule feature of git), running `./autogen.sh` will make a simple check to detect this, and then clone/checkout the two resources parallel to all language repos (if not already available). It will then make a symlink from the expected location in `dest/` to the resources one dir level up.

| Submodule           | Subtree                                            |
| ------------------- | -------------------------------------------------- |
| does not work       | works transparently                                |
| requires `./autogen.sh` | won't work with `./autogen.sh`                 |
| hard to commit/push | commits are transparent                            |
| update separately   | updates automatically                              |
## CI

See **One language, git** above. If the source code is fetched in other ways, it is the responsibility of the builder to make sure that it is available as expected at `autoreconf` time.

## tarballs

All include statements in `Makefile.am` files are processed before tarballs are made, which means that there is no pre `autoreconf` processing requirements. The tarballs can thus be built independently of the above concerns.

# Version checks

* `giella-core` will switch to use a flat incrementing version number, instead of semantic versioning as is used now
* `configure.ac` (and related files) check that the available version of both resources are the correct one, as usual

All-encompassing updates to required versions can easily be done using the [dadmin tool](https://github.com/divvun/project-dadmin/).
