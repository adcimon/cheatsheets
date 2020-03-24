# Mercurial

[Mercurial](https://www.mercurial-scm.org/) is a free, distributed source control management tool.

## Configuration

Configure mercurial.
```
hg config --edit
```

## Create repositories

Create a new repository.
```
hg init
```

Download a repository.
```
hg clone repository
```

## Branches

Create a new branch.
```
hg branch name
```

Switch to the specified branch.
```
hg update branch
hg checkout branch
```

Combine the specified branch's history into the current branch.
```
hg merge branch
```

## Make changes

Add the specified files on the next commit.
```
hg add file
hg add
```

Commit the specified files in version history.
```
hg commit -m "Message"
```

## Synchronize changes

Upload all local branch commits.
```
hg push
```

Update your current local working branch with all new commits from the corresponding remote branch.
```
hg pull
```

## Show changes

Show changed files in the working directory.
```
hg status
```

Show revision history of the repository.
```
hg log
```

Show revision history of a file.
```
hg log --follow file
```