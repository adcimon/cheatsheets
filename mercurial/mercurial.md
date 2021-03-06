# Mercurial

<p align="center"><img align="center" src="mercurial.png"></p>

[Mercurial](https://www.mercurial-scm.org/) is a free, distributed source control management tool.

## Table of Contents

* [Configuration](#configuration)
* [Repositories](#repositories)
* [Branches](#branches)
* [Tags](#tags)
* [Make changes](#make-changes)
* [Revert changes](#revert-changes)
* [Synchronize changes](#synchronize-changes)
* [Show changes](#show-changes)

## Configuration

Configure mercurial.
```
hg config --edit
```

## Repositories

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
hg commit -m "New branch"
hg push --new-branch
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

## Tags

Create a tag.
```
hg tag [--local] <name>
hg push
```

Remove a tag.
```
hg tag --remove <name>
hg push
```

Shows the tags.
```
hg tags
```

## Make changes

Add the specified files on the next commit.
```
hg add <file>
hg add
```

Commit the specified file or directory in version history.
```
hg commit <file|directory> -m "Message"
```

Commit all the files and directories in version history.
```
hg commit -m "Message"
```

Commit also the added or deleted files in version history.
```
hg commit --addremove -m "Message"
```

## Revert changes

Discard local changes of a file.
```
hg revert -C <file>
```

Discard all local changes.
```
hg revert --all
```

Revert changes between 2 commits.
```
hg diff -r <from_changeset> -r <to_changeset>
hg diff -r <to_changeset> -r <from_changeset> > revert.patch
hg import revert.patch
hg out
hg push
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
hg update
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
hg log -l <n>
```

Show revision history of a file.
```
hg log --follow <file>
```

Show current commit changeset.
```
hg id -i
```
