# Motivation

There have been a number of factors behind the decision to move to GitHub, the following are the main ones:

* requests
* better visibility and code accessibility
* more integration opportunities
* easier user management & access control
* better release management

## Requests

Over the last couple of years there has been a steady flow of requests for getting access to our code in GitHub.

## Visibility and accessibility

Although the Divvun and Giellatekno groups have always been following an open source filosophy, and all our code is open source, it has been hard to find and access. This has also influenced the possible reuse of our code and tools by other projects.

By moving to GitHub, we believe that our code will be much more visible and much easier to findg, and thus lead to increased collaboration.

## Integration opportunities

Integrating our code in other projects have been possible for a long time, especially thanks to the effort by Tino Didriksen. It has nevertheless been a bit arcane and hard to do, and it has been way too much work to e.g. get a package uploaded to [zenodo.org](https://zenodo.org). By moving to GitHub, integration with other services should be easier, as well as integration with other projects.

## User management

In GitHub, everyone manages their own account, instead of us having to manage subversion users. Also, creating teams and repository access based on team membership is easy, and will be made possible from the command line via a new tool developed for us.

The one thing that is still not easily possible is to email all members of an organisation, to draw attention to major news, events or disrupting changes that are coming.

## Release management

`git` and `git-flow` allows for a controlled and easy separation of development, releases and bug fix branches, making it much easier to release early and often without loosing control.
