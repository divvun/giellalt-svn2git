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

## Example: sme

```bash
cut -d'#' -f1 < $GTPRIV/admin/svn/svn2git-authors.txt \
	> svn2git-authors.txt
```

Clone the complete repo, to be able to extract gt/sme

```bash
git svn clone https://gtsvn.uit.no/langtech/trunk \
    --authors-file=svn2git-authors.txt langtech
```

Copy the clone to gtsme, extract only gt/sme. By copying the clone,
the langtech directory can be used as the base for extracting
the other languages inside gt/

```bash
rsync -avpp langtech/ gtsme
cd gtsme
git filter-branch --subdirectory-filter gt/sme HEAD -- --all
```

Clone langs/sme

```bash
cd ..
git svn clone https://gtsvn.uit.no/langtech/trunk/langs/sme \
	--authors-file=svn2git-authors.txt lang-sme
```

Merge gtsme into lang-sme

```bash
cd lang-sme
git remote add gtsme $HOME/repos/langtech_to_github/gtsme
git checkout gtsme/master
git checkout -b gtsme
git checkout master
git merge --allow-unrelated-histories gtsme
find . -size +50M
git filter-branch -f --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch polderland/adj-sme-plx.txt' --tag-name-filter cat -- --all
git filter-branch -f --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch polderland/noun-sme-plx.txt' --tag-name-filter cat -- --all
git filter-branch -f --prune-empty --index-filter 'git rm -rf --cached --ignore-unmatch tools/spellcheckers/listbased/hunspell/nums.txt' --tag-name-filter cat -- --all
git remote add git@github.com/giellalttmp/lang-sme
git push -f origin master
```

# Preparations

* get updated GitHub email info from all - DONE to the extent it is received
* invite all relevant persons - DONE
  	* everyone with confirmed emails - DONE
  	* everyone committing since 1.1.2016 (last four years, roughly) - DONE
  	* ignore the rest, they can ask for access later
* mirror the svn repo as individual language repos - DONE for `langs/`
  	* such that only a few more commits needs to be added before switching to git
  	* make sure the `authors.txt` file is complete - DONE
* create teams - DONE
* add descriptions to all repos - DONE
* make sure CI/CD is working for both keyboards and languages - IN PROGRESS
* full history of `giella-core`, `giella-shared` & `langs-templates/und/` - DONE
* test lock master etc on the keyboard repos
* identify the correct svn co url when the default branch is not `master`

# Move steps

We do one `langs` directory at a time. First is `$GTHOME/langs`, then `$GTHOME/experiment-langs`. The actual move should take only a few hours, if not less.

1. email everyone about move time = last checkin time - DONE
1. make one final update to git, using `git svn` - DONE
1. push to GitHub
1. create branch develop, make it the default, lock master
1. move all from the **GiellaLTTmp** GitHub org to **GiellaLT**; delete the GiellaLTTmp org
1. make all repos public
1. remove `langs` and `keyboards` from svn
1. add languages to teams
1. announce the new checkout/clone url's, and reopen for edits
1. rewrite all Makefile.am files to include files from `giella-core/am-shared/`
1. Remove `am-shared/` in all languages
