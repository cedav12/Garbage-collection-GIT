# Git prune
Second most importand usecase of Git garbage collector is to remove orphaned or inaccessible commits. Git performes this operation at an assigned time automatically. This operation could be also run manually by `git prune`, which is an housekeeping feature build in `git gc` command. Command `git` will be describe in detail here.

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

![image](image.png)


