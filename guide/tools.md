# Pull Requests #

#### Mirrors and smoke ####

In the case when [GitHub is a mirror](http://blog.plataformatec.com.br/2013/05/how-to-properly-mirror-a-git-repository/) of your real git repository you can't just click "Merge" and get away with this, as changes applied directly to the repository that lives on your GitHub account won't be pushed to your canonical repo.

In such cases you need to merge the branch by yourself, through the git CLI. Jump into your shell, checkout your main branch and use ```git merge``` to merge your feature branch. Don't forget to use the ```--no-ff``` flag or turn the ```merge.ff``` configuration off.

```
  $ git checkout master
  $ git merge --no-ff your-branch
  # Or turn fast forwards off for good.
  $ git config --global merge.ff false
```

The merge commit will tell GitHub to close the Pull Request that was opened to that branch, but the branch won't be deleted automatically, and you need to delete it in your canonical repository and then delete it from the GitHub repository when the changes are replicated to GitHub.

### Using hub ###

[hub](http://github.com/github/hub) is a handy tool that wraps the ```git``` command and adds some GitHub flavoured features and shortcuts. Some of them are useful for the workflow of opening and reviewing Pull Requests.
