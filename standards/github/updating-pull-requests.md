## Updating Pull Requests

At some point our PRs will be out of sync with other branches and we will have to update them to catch up with the latest changes before merging in. You can either update via merge or rebase.

### Merge

[Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

- Non destructive (does not alter any commits)
- May be harder to navigate due to merge commit forks
- Merging `develop` *into* `feature-1`

```bash
# make sure branches are updated
git checkout feature-1
git merge develop
git push
```

- into means the branch that will receive develop’s commits
- Alternatively merging `feature-1` into `feature-2`

```
git checkout feature-2
git merge feature-1
git push
```

### Rebase

[Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

- Destructive (creates new commits in place of older ones)
- Can be easier to navigate due to not having any merge commit forks
- rebasing `feature-1` *onto* `develop`

```bash
# make sure branches are updated
git checkout feature-1
git rebase develop
# force with lease is safer than force
git push --force-with-lease
```

- onto means the branch whose commits you want to put before the target branch

### Which should I use

Generally we prefer to use rebase except for some cases where merge is more ideal

### Golden Rule of Rebasing

[Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing)

- Avoid using rebase for any branches that other branches are dependent on (we call these public branches)
- `develop`/`master`/`main` are public branches so avoid rebasing those
- Release branches are also public branches so avoid rebase for those
- Feature branches can also be public in some scenarios. For example this setup, while not exactly ideal, can happen

    ```
    develop <- feature-1 <- feature-2 <- feature-3
    ```

    - feature-1 and feature-2 are public because they branched out from other branches. Avoid rebasing these branches to avoid conflicts. Prefer merge for this case if you need to update.
    - It’s especially important to avoid rebase if these PRs are separate tickets to preserve prior merge commits and leave traces of where these started/ended
    - feature-3 is not public so rebase should be fine
