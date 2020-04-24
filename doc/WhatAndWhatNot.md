# What is moved and what is not

## Being moved

The following is moved from [our Subversion repository](https://gtsvn.uit.no/langtech/)
to [github.com/giellalt](https://github.com/giellalt):

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
* `giella-libs` (perhaps not this one, it is a relict of our old build setup, and will
   be irrelevant in the future)
* `giella-shared`
* `giella-templates`

## NOT being moved

Essentially everything else in `$GTHOME` will be left in svn, at least for now. Most of
these things are also specific to Tromsø, with the exception of `$GTHOME/words`. That
one will be considered for a move to github at a later point in time.

# Things being discarded in the move

* Users with only a single or a few test commits
* svn branches (they have been reviewed; since the svn repo will still be accessible,
  those interested in the branches and the history can access them there)
* svn tags (they have also been reviewed, with the same conclusion as for branches)

These are still available in the svn repo, if need be.

## Duplicate language dirs / repos

Some languages have more than one description, for various historical reason.
They are the following:

- est
- esu
- fin
- smn
- sms
- zul

### est

In `langs/est/` and `experiment-langs/est/`.

Two independent implementations of an Estonian analyser, and both should be kept. Their
names should be something like `est-x-XXX`, where `XXX` is specific for each variant.
The variant names will be:

- `lang-est-x-plamk` = old `langs/est/`
- `lang-est-x-utee` = old `experiment-langs/est/`

### esu

There's an old initial setup in `startup-langs/esu/`, but with minimal actual work.

The other one is new work by Lonny Alaskuk Strunk, which he has now included in our
infra (directly to GitHub).

The old empty framework is deleted, with the exception of `src/morphology/root.lexc`,
which is moved to `$GTHOME/restlangs/` for future reference.

### fin

- in `langs` - a fork of [omorfi](https://github.com/flammie/omorfi)
- in `experiment-langs` - essentially just to keep a copy of Fred Karlsson's
  original CG1 Finnish Constraint Grammar file. The rest is tentative work, but
  not substantial.

The FINCG file has been moved to `langs/fin/doc/`, and the rest of
`experiment-langs/fin/` has been removed and will not be transferred to github.

### smn

- in `langs` - this is the main development line
- in `experiment-langs/smn-ex/` - this was an experiment with alternative two-level
  rules. Removed in accordance with the responsible person.

### sms

- in `langs` - this is the main development line
- in `experiment-langs` - this was an experiment, and has been removed.

### zul

There's a closed-source repo with material donated from the University of South Africa.
This will be turned into a private repo with the name `lang-zul`.

Then there is some initial work in `startup-langs/zul/`, which should be kept.
It should be converted to a public repo with the name `lang-zul-x-exp`.
