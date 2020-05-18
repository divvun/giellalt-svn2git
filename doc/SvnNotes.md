# `svn` usage notes

svn ignores must be set anew, it is not transferred by `git svn`.

Command:

```
$GTHOME/giella-core/scripts/set-svn-ignores-langs.sh .
```

for each repo.

# svn check-out

```
svn co https://github.com/giellalt/lang-XXX.git/trunk lang-XXX
```

Replace `XXX` (two places above) with your ISO-639 3-letter language code.
