# Mirroring a git repository properly

G'day Internet.

Two weeks ago my company migrated from Github Entreprise to Github Enterprise Cloud. All the migration went well. Only today I realised that two of my private repositories were not migrated. Luckily enough a colleague of mine pointed me towards a solution (thanks Dario). And here I share this solution with you.

Making a simple copy of the repository and pushing it to a new repository in the cloud was a solution, but not a good one. Why? Because all the history of the repository is lost. Our solution does not only copy the codebase, but also the history.

First we want to retrieve the old repository. In a terminal, run the following command.

```zsh
λ git clone --mirror git@company.com/repository.git
```

Note the [--mirror](https://git-scm.com/docs/git-clone#Documentation/git-clone.txt---mirror) option. A new `repository.git` folder is created, it contains both the codebase and the history.

Before running the next commands, we need to create an empty repository in github cloud. If you wanted to change the name of you repository, now is a good time. For this example we will keep the name `repository`.

Once it is create run the following commands

```zsh
λ cd repository.git
λ git push --mirror git@github.com:company/repository.git
```

We should now be able to see our repository in github cloud populated with the codebase and the history. 

When pushing to the new repo we could encounter the following error
```
! [remote rejected] refs/pull/1/head -> refs/pull/1/head (deny updating a hidden ref)
```
This is likely because a [pull request was opened](https://stackoverflow.com/a/34266401) at the previous repository.

That's all folks

Jon
