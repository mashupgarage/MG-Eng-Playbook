# Updating Pull Requests

At some point our PRs will be out of sync with other branches and we will have to update them to catch up with the latest changes before merging in. You can either update via merge or rebase.

## Merge

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

- Into means the branch that will receive develop’s commits
- Updating nested branches via merge

  Given branch structure:
  ```
  develop <- feature/dashboard <- feature/posts <- feature/comments
  ```
  Update each branch
  ```bash
  # make sure develop is updated
  git checkout feature/dashboard
  git merge develop
  git push

  git checkout feature/posts
  git merge feature/dashboard
  git push

  git checkout feature/comments
  git merge feature/posts
  git push
  ```

## Rebase

[Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

- Destructive (creates new commits in place of older ones)
- Prone to breakage and conflicts if not managed properly
- Can be easier to navigate due to not having any merge commit forks
- Rebasing `feature-1` *onto* `develop`

	```bash
	# make sure branches are updated
	git checkout feature-1
	git rebase develop
	# force with lease is safer than force
	git push --force-with-lease
	```

- Onto means the branch whose commits you want to put before the target branch

## Rebase Do's and Don'ts

- ✅ Branch with no comments

  When a branch is in WIP stage, rebase should be fine. You can use it to clean up commits and update to develop without worry of breaking commits for anyone else.
- ✅ Approved branch

  Once branch has passed review and is ready to merge, you can use a rebase to update and clean up the branch before merging to develop.
- ❌ Nested branch
  ```
  develop <- feature/dashboard <- feature/posts <- feature/comments
  ```

  Avoid doing this

  ```
  git checkout feature/comments
  git rebase develop
  git push --force-with-lease
  ```

  Since `feature/dashboard` and `feature/posts` don't have develop's changes yet, `feature/comments` will not be compatible to merge into them later. Update via merge instead (see `Updating nested branches via merge` above).
- ❌ Branch authored by someone else
  ```
  develop <- feature/dashboard (written by teammate)
  ```

  Avoid doing this

  ```
  git checkout feature/dashboard
  git rebase develop
  git push --force-with-lease
  ```

  This will create new commits in `feature/dashboard` which will not be compatible with the commits in the local branch when they pull the updated version. Prefer merge instead.
- ❌ Parent branch
  ```
                                feature/posts
                               /
  develop <- feature/dashboard
                               \
                                feature/css-layout
  ```
  Avoid doing this

  ```
  git checkout feature/dashboard
  git rebase develop
  git push --force-with-lease
  ```
  Rebase will create new commits in `feature/dashboard` but `feature/posts` and `feature/css-layout` will still look for the old commit references which is prone to conflicts. Prefer to update via merge.
- ❌ Nested rebase
  ```
  develop <- feature/dashboard <- feature/posts <- feature/comments
  ```
  Avoid doing this
  ```bash
  git checkout feature/dashboard
  git rebase develop
  git push --force-with-lease

  git checkout feature/posts
  git rebase feature/dashboard
  git push --force-with-lease

  git checkout feature/comments
  git rebase feature/posts
  git push --force-with-lease
  ```
  Note that this may still work without issues in some cases but is very prone to conflicts especially if branch is really outdated. For big branches it's not worth the hassle. Update via merge instead (see `Updating nested branches via merge` above).


## Golden Rule of Rebasing

[Merging vs. Rebasing | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing)

- Avoid using on PRs that have comments as this can remove comments that reviewers may need to follow up on
- Avoid using rebase for any branches that other branches are dependent on (we call these public branches)
- `develop`/`master`/`main` are public branches so avoid rebasing those
- Release branches are also public branches so avoid rebase for those
- Branches not authored by you are public branches
- Feature branches can also be public in some scenarios, even if you authored them. For example this setup, while not exactly ideal, can happen

    ```
    develop <- feature-1 <- feature-2 <- feature-3
    ```

    - feature-1 and feature-2 are public because they branched out from other branches. Avoid rebasing these branches to avoid conflicts. Prefer merge for this case if you need to update.
    - It’s especially important to avoid rebase if these PRs are separate tickets, to preserve prior merge commits and leave traces of where these started/ended
    - feature-3 is not public so rebase should be fine
