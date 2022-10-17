# Garbage-collection-GIT
The concept of the garbage collection cames from computer science and serves as automatic memory manager. This concept is used for instance in interpreted programming languages, which use dynamic memory allocation, such as Java or C#. GC enables cleening up the memory space dedicated to objects, that are not already used.

Git garbage collection is an automatic operation, which is performed by Git from time to time in order to clean the repository. Git GC has two most important usecases, which will be describe in this repository. Firstly `git gc ` streamlines repository storage by performing compression on objects in git repository, which saves storage space. Git GC removes duplicated objects, leaves just the most current object and its predecessors are left in the size of difference between older and newer version. By these objects are meant all basic objects of git data structere - **Directed Acyclic Graph** - `commit`, `tree` and `blob`. In addition `git gc` removes orphaned commits or commits inaccessible by any references. Orphaned objects or unreachable references are stored in the so-called `git reflog`. *Garbage objects* are eventually moved to pack folder (` .git/objects/pack`), and Git can still unpacked them. Even though git garbage collection is performed automatically, it can be also run manually in `git bash` by the command `git gc` and [`git prune`](git-prune.md). Relationship between these two commands is *parent-child*. Command `git gc` runs also `git prune` defautly, therefore it is not common to use `git prune` separately. 

### Sources
https://www.atlassian.com/git/tutorials/git-gc

https://www.geeksforgeeks.org/git-gc-garbage-collection/

https://git-scm.com/docs/git-prune

https://www.geeksforgeeks.org/git-git-prune/

https://www.atlassian.com/git/tutorials/git-prune

