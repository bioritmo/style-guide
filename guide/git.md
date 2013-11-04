# Git #

* Always use the company's e-mail for projects commits;
* Create feature branches for your work;
* Use a global [gitignore to ignore](https://help.github.com/articles/ignoring-files) files that are specific to your environment (editor settings, unwanted system files, etc.);

* Name your branches using ```-``` to separate words;

```
  $ git checkout -b my-feature-branch
```

* Whenever you need to merge upstream updates into your feature branch, do it with ```rebase```, unless there are other people working on that same branch (in that case, discuss with them when it will be a good moment to rebase), or when there is an open pull request related to that branch;

```
  $ git checkout master
  $ git pull --rebase
  $ git checkout my-feature-branch
  $ git rebase master
```

* When merging your branch back to master, make sure to create a merge commit. This way you make it easier to track, visualize and revert features added to the master branch. Run ```merge``` on master with:

```
  $ git checkout master
  $ git merge --no-ff my-feature-branch
```

* To make sure you don't forget to add both ```--rebase``` when pulling and ```--no-ff``` when merging, we strongly recommend that these settings are pre-configured globally, as follows:
```
  $ git config --global pull.rebase true
  $ git config --global merge.ff false
```

* Delete feature branches both local and remote after merging.

* Good commit messages include a nice summary and subsequent information if needed; The summary must give you a quick overview of the commit and the subsequent text may include further explanation ('why this commit was necessary ?'). Read more [here](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).

* Use ```simple``` for your ```push.default``` option. This way you'll only push branches that are explictly tracked with your local branches and that have the same name as the remote ones.

```
  $ git config --global push.default simple
```

The default is ```matching``` which will push all branches that have the same name as remote ones, potentially messing with the remote branches. Git 2.0 will change the default to ```simple``` as well. You can read about these options at the [git-config manual page](http://git-scm.com/docs/git-config.html).
