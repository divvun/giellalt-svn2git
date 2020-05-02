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
cut -d'#' -f1 < $GTPRIV/admin/svn/svn2git-authors.txt > svn2git-authors.txt
```

Clone the complete repo, to be able to extract gt/sme

```bash
git svn clone https://gtsvn.uit.no/langtech/trunk  --authors-file=svn2git-authors.txt langtech
```

Copy the clone to gtsme, extract only gt/sme. By copying the clone,
the langtech directory can work be used as the base extracting
the other languages from gt/

```bash
cd ..
rsync -avpp langtech/ gtsme
cd gtsme
git filter-branch --subdirectory-filter gt/sme HEAD -- --all
```

Clone langs/sme

```bash
git svn clone https://gtsvn.uit.no/langtech/trunk/langs/sme lang-sme  --authors-file=svn2git-authors.txt langtech
```

Merge gtsme into lang-sme

```bash
cd ../lang-sme
git remote add gtsme /home/boerre/repos/langtech_to_github/gtsme
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
