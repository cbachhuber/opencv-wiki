OpenCV repository have several branches with different contribution policies.

### Common rules for all branches

* Your development branch name must differ from the names of branches in the central OpenCV repository, i.e. your branch must not be named _2.4_, _3.4_ or _master_ (it's technical requirement specific to our continuous integration system)
* Multiple related commits should be [squashed](http://git-scm.com/book/en/Git-Tools-Rewriting-History#Squashing-Commits) into one. Pull request must contain either a single commit, either several unrelated commits.

### 2.4

This is branch for 2.4.x releases.

* Only critical bugfixes will be accepted

### 3.4

This is branch for 3.4.x releases.

* ABI compatibility must be preserved
* We will merge changes from _3.4_ into _master_ regularly (weekly/bi-weekly), so if your pull request is applicable to both branches, you should choose _3.4_ branch as base, not _master_.

### master

This is current development branch for 4.x releases.

* API compatibility must be preserved
* If your pull request is also applicable to _3.4_ branch, you should choose that branch as "base"
* If you've already created pull request based on _master_ branch, but it is also applicable to _3.4_ branch you will be asked to rebase it to 3.4, see the instruction in the following section.

### Rebase pull request from _master_ to _3.4_

_If you can not do it by yourself, please ask maintainers for help._

* do not close existing pull request
* change "base" branch of the pull request
  * press "Edit" button near the pull request title
  * choose "3.4" from the dropdown list
* rebase your commits from master onto 3.4 branch
  * `git checkout <your-branch>`
  * (optional) create backup branch: `git branch <your-branch>-backup`
  * `git remote update upstream` (assuming _upstream_ [is pointing](https://help.github.com/articles/configuring-a-remote-for-a-fork/) to `opencv/opencv` GitHub repository)
  * `git rebase -i --onto upstream/3.4 upstream/master`
  * editor will be opened, check list of commits - there should be only your commits, save and exit
  * `git push --force origin <your-branch>` (assuming _origin_ [is pointing](https://help.github.com/articles/configuring-a-remote-for-a-fork/) to `<your-username>/opencv` GitHub repository)

### Related articles

* [GitHub Flow](https://guides.github.com/introduction/flow/) guide
* [Forking Projects](https://guides.github.com/activities/forking/) guide
* [ABI Compliance Checker](https://lvc.github.io/abi-compliance-checker/) tool
