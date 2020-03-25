# What is moved and what is not

## Being moved

The following is moved from [our Subversion repository](https://gtsvn.uit.no/langtech/) to [github.com/giellalt](https://github.com/giellalt):

The `*-langs` directories:

* `closed-langs` (will become private repos)
* `closedSA-langs` (will become private repos)
* `experiment-langs`
* `external-langs`
* `langs`
* `startup-langs`

The `*-keyboards` directories have already been moved.


The shared `giella-*` directories:

* `giella-core`
* `giella-libs` (perhaps not this one, it is a relict of our old build setup, and will be irrelevant in the future)
* `giella-shared`
* `giella-templates`

## NOT being moved

Essentially everything else in `$GTHOME` will be left in svn, at least for now. Most of these things are also specific to Tromsø, with the exception of `$GTHOME/words`. That one will be considered for a move to github at a later point in time.

# Things being discarded in the move

* Users with only a single or a few test commits
* svn branches (they have been reviewed; since the svn repo will still be accessible, those interested in the branches and the history can access them there)
* svn tags (they have also been reviewed, with the same conclusion as for branches)

These are still available in the svn repo, if need be.
