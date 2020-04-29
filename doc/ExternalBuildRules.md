# External build rules

To enforce true language independence for the core build rules, they should be moved out of each language dir (`am-shared/`) to `giella-core/am-shared`. There is also a separate repo (`giella-shared`) of shared language resources (language data such as digits, names or acronyms, or shared filter regexes), these should be treated the same way wrt building. To make automatic builds work from source check-out or clone, there are a number of things to consider.

# Problem

`am-shared` is needed at `autoreconf` time, which requires that all build resources are available at a known and relatively local position. This makes sharing the resources among languages more tricky, since every language is its own repository in GitHub. Thus these resources are not automatically available by just checking out the language repo, which means that the language tools can not be built.

Using environment variables is not ideal, since we would have to rely on them all the time, for all builds (given that the resources must be available for `autoreconf`).

# Basic idea

> `giella-shared` & `giella-core` as git submodules or subtrees in each language. This can be overriden by `autogen.sh` for each language, see below.

Both resources should available in a dir `deps/` in each language, so that the path to the build resources will always be: `$(top_srcdir)/deps/giella-core/am-shared/*`, and similar for `giella-shared`.

# Usage scenarios

## One language

### Cloning using git

If cloned with submodules, everything will be in place, and nothing more needs to be done.

If cloned without submodules, running `./autogen.sh` will clone the required resources and make them available in the correct place.

### Checking out using svn

The `svn` interface of GitHub does not give access to submodules. Instead the resources will be checked out by `./autogen.sh` and made available in the correct place.

## Multiple languages

If many languages are cloned or checked out in parallel (and without the submodule feature of git), running `./autogen.sh` will make a simple check to detect this, and then clone/checkout the two resources parallel to all language repos (if not already available). It will then make a symlink from the expected location in `dest/` to the resources one dir level up.

## CI

See **One language, git** above. If the source code is fetched in other ways, it is the responsibility of the builder to make sure that it is available as expected at `autoreconf` time.

## tarballs

All include statements in Makefile.am files are processed before tarballs are made, which means that there is no pre `autoreconf` processing requirements. The tarballs can thus be built independently of the above concerns.

# Version checks

* each langauge tied to a specific version of giella-core?
* giella-core using a flat incrementing version number, no semantic versioning
* configure.ac (and related files) check that the available version of both resources are the correct one
