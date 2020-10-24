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
hg clone <repository>
```

## Branches

List all branches.
```
hg branches
```

Create a new branch.
```
hg branch <name>
```

Switch to the specified branch.
```
hg update <branch>
hg checkout <branch>
```

Combine the specified branch's history into the current branch.
```
hg merge <branch>
```

## Make changes

Add the specified files on the next commit.
```
hg add <file>
hg add
```

Commit the specified files in version history.
```
hg commit -m "Message"
```

Commit the deleted files in version history.
```
hg commit --addremove -m "Message"
```

## Synchronize changes

Upload all local branch commits.
```
hg push
```

Push a new branch.
```
hg push --new-branch
```

Update the working directory with all new commits from the corresponding remote branch.
```
hg pull
```

Update the working directory at the changeset point.
```
hg update -C <changeset>
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
hg log --follow <file>
```

Show current commit.
```
hg id -i
```

## Tags

Create a tag.
```
hg tag [--local] <name>
```

Remove a tag.
```
hg tag --remove <name>
```

Shows the tags.
```
hg tags
```