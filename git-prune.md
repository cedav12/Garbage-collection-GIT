# Git prune
Second most important usecase of Git garbage collector is to remove orphaned or inaccessible commits. Git performes this operation at an assigned time automatically. This operation could be also run manually by `git prune`, which is an housekeeping feature build in `git gc` command. Command `git` will be describe in detail here.

## Orphaned commits
Orphaned commits are commits inaccessible by any references. This situation could occur, when commands altering history such as `git reset` or `git rebase` are used.

We can see how oprphaned commits could occur on the folowing example:

1. Create git repository with text file `git-prune.txt` a modify it, which will create two commits in the repository:

`$ mkdir git-prune`

`$ git innit`

`$ touch git-prune.txt`

`$ git add git-prune.txt`

`$ git commit git-prune.txt -m "git-prune.txt added"`

`$ echo "Hello git-prune.txt" > git-prune.txt`

`$ git commit git-prune.txt -m "git-prune.txt modified"`

2.  Run `git log`:

`$ git log`

**Output:**

![image](screenshot1.png)

* Here the git bash displays commit history of our repository.

3. Now we make the second commit unreachable.

`$ git reset --hard 0905dc3`

`$ git log`

**Output:**

![image](screenshot2.png)

* Here can be seen that references no more points at the second commit. Commit could be still reachout by command `git checkout <commit 2 hash>`, but now the commit is detached from the main branch.

## Git prune
`git prune` is a command included in its parent command `git gc`. Git prune prunes all unaccessible objects form repository. The aim of this is to clean the working directory and prevent it from being chaotic. Git garbage collection automatically from time to time (which is defaultly set) detects unreachable objects and move them to pack file (these objects could by located by command `git prune-packed`). Usally there is no need to use directly `git prune`, `git gc` should be run instead. We will see on the example below how does the `git prune` command works:

`$ git prune --dry-run --verbose`

* Here empty output could be seen. This means that no commit is so far to be pruned, therefore git prune will not delete anything. The reason behind this is that the reference to the orphaned commit is still maintained in `git reflog`. In order to delete the commit we should firstly clear the git reflog. To do so we should force git reflog to expire (which would otherwise happen after some time). This is not recommended to do during the basic workflow, especially, when you work in team on some project, because it could be confusing for other collaborators and some important object could be unintentionally lost.

`$ git reflog expire --expire=now --expire-unreachable=now --all`

* Now we are ready to prune the second commit.

`$ git prune --dry-run --verbose`

**Output:**

![image](screenshot3.png)

* Finally we can see hashes of objects associated with the second commit, which is about to be removed. Now we could remove the seccond commit using the `git prune` command.

## Git prune options
There are several methods how to use `git prune`. Most used ones will be described below. 

`-n --dry-run`

* The command we have used above. This command will not remove anything, just displays objects which would be about to be removed.

`-v --verbose`

* Reports all objects, that would be affected by the git prune *--option* command.

`--expire <time>`

* Objects older than *<time>* expire.

## Summary
The `git prune` is a git command, that serves as cleaning method of git repository. Usually there is no need to run directly `git prune` because it is included in its parent command `git gc`. The usecase of the `git prune` command is to remove orphaned or unreachable objects, which usually occurs from the action of altering history by commands such as `git reset` or `git rebase`.