# Git  

## Fork + Rebase Workflow 
The fork and rebase workflow is a nice way to keep the git history of a project clean and linear. 
It uses forked repos to isolate changes so that one contributor's branches don't pollute another person's local repo.

IMPORTANT: This should only be done with forked repos. It is very annoying to use on a shared repo.
This workflow is based on this blog post: https://medium.com/@ruthmpardee/git-fork-workflow-using-rebase-587a144be470

### Fork setup 
First, fork the repo that you're going to work on in Github.
Then, clone that repo to your local machine and set the "upstream" repo, so git knows where the original repo lives:
```
git clone [url of fork repo]
git remote add upstream [url of official upstream repo]
```

### Working on a new feature
Create a branch to start work on a new feature.
```
git co master
git pull upstream master

# Create and checkout to new feature branch
git co -b my_new_feature

# Do some work and commit it...
...
git add [...]
git commit -m 'commit message'

# Push to remote branch on your fork
git push origin my_new_feature

# Do PR stuff and rebase onto master when accepted...
...
```

### Pulling in upstream changes 
If master has new commits while you're working on your feature, you need to pull those changes and rebase onto rebase your branch onto master.
```
git co my_new_feature 

# While on your feature branch pull the official repo's master changes:
git pull --rebase upstream master

# Resolve potential merge conflicts...
...

# Sync the local rebase of your branch to the remote fork repo.
# You need to use --force or -f since history is being rewritten, so make sure no one else is using this branch. 
# Since this is a fork, no one else should be using the branch anyway.
git push -f origin my_new_feature
```

### Resolving merge conflicts 
With the rebase workflow, git adds your commits on top of master one at a time.
If there's a conflict, it pauses the rebase so you can fix it.
```
# Once the merge conflicts are fixed, add the changes to mark them as resolved
git add [...]
git rebase --continue 

# Sync the local rebase of your branch to the remote fork repo.
# You need to use --force or -f since history is being rewritten, so make sure no one else is using this branch. 
# Since this is a fork, no one else should be using the branch anyway.
git push -f origin my_new_feature
```

### Cleanup 
When your feature is done, approved, and merged into the upstream master, clean up your local and remote repos. 

```
# Once the PR is approved and merged into upstream master, bring your local repo's master up to date:
git pull upstream master

# Bring your forked remote repo's master branch up to date:
git push origin master

# Clean up the feature branches (local, local ref to remote origin, remote origin)
git branch -D my_new_feature
git branch -dr origin/my_new_feature
git push --delete origin my_new_feature
```

## Miscellaneous Workflows 

### Amend a branch commit
Sometimes you want to modify a commit that is already in a branch that you pushed to your remote. 
Maybe because you made a typo or just need to change small things that are still topically related to the commit you pushed.
You can amend the commit and push it to make these types of changes.

```
# On your feature branch, do the work you want to amend to a given commit.
git add [...]
git commit --amend [...]

# Need to force since we're updating history of a commit that's already in the remote branch:
git push --force origin my_new_feature
```

### Squash commits 
Sometimes you may want to fold / squash several commits into a single commit. Git has an interactive rebase mode to provide that functionality. 
```
git rebase -i HEAD~[# of commits to squash]
```

In the interactive editor, mark the head commit as "pick" or "p" and the preceding commits as "squash" or "s".

## Aliases 
Aliases are stored in `~/.gitconfig`. These are some common ones that I have aliased:

```
[alias]
	co = checkout
	br = branch
	ci = commit
    # Add modified / deleted files to staging and commit
	ca = commit -a
	st = status
	amend = commit --amend --no-edit
	prev = checkout HEAD^
	unstage = restore --staged
	graph = log --all --graph --decorate --oneline
```

## Worktrees
* 
* A simple setup for worktrees: https://morgan.cugerone.com/blog/how-to-use-git-worktree-and-in-a-clean-way/
* Using remotes with worktrees: https://morgan.cugerone.com/blog/workarounds-to-git-worktree-using-bare-repository-and-cannot-fetch-remote-branches/
