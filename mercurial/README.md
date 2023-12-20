# Mercurial

<p align="center"><img align="center" width="30%" height="30%" src="assets/mercurial.svg"></p>

[Mercurial](https://www.mercurial-scm.org/) is a free, distributed source control management tool.

## Index

* [General](#general)
* [Repositories](#repositories)
* [Branches](#branches)
* [Tags](#tags)
* [Make changes](#make-changes)
* [Revert changes](#revert-changes)
* [Synchronize changes](#synchronize-changes)
* [Show changes](#show-changes)
* [Merge branches](#merge-branches)

## General

Configure mercurial.
```
hg config --edit
```

Ignore SSL certificate error `[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate`.
```
--insecure
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

hg update -C <branch>
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

Revert last local commit.
```
hg rollback
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

Update the working directory with all new commits from the corresponding remote branch.
```
hg pull
hg update
```

Update the working directory at the changeset point.
```
hg update -C <changeset>
```

Update the working directory at the last changeset.
```
hg update -C
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

## Merge branches

Merge 2 branches.
```
hg merge <branch>
hg commit -m "Merge branch into current branch"
hg push
```

List conflicts.
```
hg resolve --list
```

Resolve a conflict.
```
hg resolve --mark <file>
```
