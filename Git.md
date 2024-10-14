# Git

## Create new branch

- `git branch <branch-name>`: creates a new branch but stays in the current one.
- `git checkout -b <branch-name>`: creates a new branch and switches to it.
- `git switch -c <branch-name>`: creates a new branch and switches to it.

## Switch between branches

- `git checkout <branch-name>`
- `git switch <branch-name>`

## Delete a branch

- `git branch -d <branch-name>`: deletes the branch if all of its changes have been incorporated into another branch.
- `git branch -D <branch-name>`: Force deletes a branch, regardless of its merge status.

## Garbage collector

- `git gc`: This command performs the Git garbage collection process, which includes tasks such as removing unreachable objects, compressing objects, and aggregating packs.
- `git gc --auto`: This command performs the same tasks as git gc, but it only runs if the repository is in a state where it needs to be optimized.

## Undo commit

- `git reset <commit>`: Uses mixed.
- `git reset --soft <commit>`: Moves the current branch pointer to the specified commit, but keeps the changes staged and in the working directory, so you can commit them again later.
- `git reset --mixed <commit>`: Moves the current branch pointer to the specified commit and un-stages the changes in the working directory; but keeps the changes as modified files.
- `git reset --hard <commit>`: Discards all changes, including the committed changes and the changes in the working directory.

## Tagging

- `git tag <tag-name> <commit-id>`

## Stash

- `git stash`: Save changes that have not been committed to a temporary area
- `git stash apply`: Restores the changes to the working directory.
- `git stash branch <branch-name>`: Applies the changes to a different branch.
- `git stash list`: Shows a list of all stashes in your Git repository, along with some information about each stash.
- `git stash apply stash@{index}`: Checkout a specific stash.
- `git stash drop stash@{index}`: Removes a specific stash.
- `git stash pop`: Retrieves a stash and removes it from the stash list in a single operation (combination of apply and drop)
- `git stash pop stash@{index}`: Pops a specific stash.

## Cherry-pick

Pick and choose specific commits from one branch and apply them to another branch, preserving the entire Git history.

- `git cherry-pick <commit-hash>`

## Switch remote repository

- `git remote set-url origin git@gitlab.com:XXXXX`

## Modify the most recent commit

- `git commit --amend`

## Revert all local changes

- `git checkout .`

## Remove file from last commit

```shell
git rm —-cached <file-to-remove>
git commit —-amend
```

## Remove files that are listed in the .gitignore but are still on the repository

```shell
git rm -r --cached .
git add .
git commit -m "Removing all files in .gitignore"
```

## Git Submodules

```shell
git submodule add git@gitlab.com:real2u/hana3d.git
```

### Clone with submodules

```shell
git clone --recurse-submodules https://github.com/chaconinc/MainProject
```

### Init and update submodules

```shell
git submodule update --init --recursive
```

## Delete local Git branches that were deleted on remote repository

```shell
git remote prune origin && git branch -vv | grep ': gone]'|  grep -v "\*" | awk '{ print $1; }' | xargs -r git branch -d
```

## File permissions when pushing on Windows

```shell
git update-index --chmod=+x <file>
```

## Create empty branch

```shell
git checkout --orphan empty-branch
git rm -rf .
git commit --allow-empty -m "root commit"
git push origin empty-branch
```

## Merge Strategies

### Fast-forward

A Fast-Forward merge can occur when there is a linear path from the current branch tip to the target branch. In this method, Git does NOT create a new commit, and just moves (i.e., fast forwards) the current branch tip up to the target branch tip.

### 3-way merge

When there is not a linear path to the target branch, Git has no choice but to combine them via a 3-way merge. 3-way merge is used to combine the changes from two branches that have diverged from a common ancestor branch. In this method, Git uses three commits to generate the merge commit: the two branch tips and their common ancestor.

### Recursive merge

The recursive merge algorithm first performs a 3-way merge between the current branch and the branch you want to merge. If conflicts are encountered, the recursive merge algorithm tries to resolve the conflicts by calling itself recursively on the sub-branches. The algorithm stops when all conflicts are resolved or when it runs out of sub-branches to merge.

## Merge vs Rebase

- `git merge` integrates changes by creating a new merge commit that ties together the history of both branches. It results in a non-linear history with multiple branches and merge commits.
- `git rebase` replays the changes from a branch onto another branch. It eliminates merge commits and makes the history linear, as if the changes were made at once.
- In simple terms, git merge results in a more comprehensive and readable history with multiple merge commits, while git rebase creates a cleaner, linear history with fewer commits.

## Pull vs Fetch

### Git fetch

- Downloads the latest changes from the remote repository; but does not merge them into your local branches.
- Leaves your local branches in their current state, allowing you to review the changes and decide how to integrate them later.
- Safe to use, as it does not modify your local branches.

### Git pull

- Downloads the latest changes from the remote repository and immediately merges them into the current branch.
- Automatically integrates the remote changes into your local repository, potentially causing conflicts if the changes cannot be merged cleanly.
- Convenient to use; but can lead to conflicts if the remote changes are not compatible with your local changes.

## Reset vs Revert

### Git revert

- Undoes changes by creating a new commit that reverses the changes in a previous commit.
- Leaves a historical record of the changes that were made and undone.
- Safe to use, as it does not destroy any history or change the repository’s permanent record.
- Useful for undoing changes that have been pushed to a remote repository, as it maintains a clear historical record of the changes.

### Git reset

- Undoes changes by moving the current branch pointer to a previous commit, effectively discarding any commits made after that point.
- Destroys the history of the discarded commits and permanently removes them from the repository.
- Dangerous to use, as it can destroy important history and make it difficult or impossible to recover the discarded changes.
- Useful for undoing local changes that have not been pushed to a remote repository, as it allows you to start over from a clean state.
