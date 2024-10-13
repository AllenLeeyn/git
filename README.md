# git

## Setting Up Git
- Configure Git with your username and email address.
```console
leeyn@SKUllZ MINGW64 ~
$ git config user.name
leeyn

leeyn@SKUllZ MINGW64 ~
$ git config user.email
leeyn.shun@gmail.com
```
---

## Git commits to commit
- Within the work directory, establish a subdirectory named hello. 
```console
leeyn@SKUllZ MINGW64 ~
$ mkdir work

leeyn@SKUllZ MINGW64 ~
$ cd work

leeyn@SKUllZ MINGW64 ~/work
$ mkdir hello

leeyn@SKUllZ MINGW64 ~/work
$ cd hello
```

- Inside this directory, generate a file titled hello.sh and input the following content: 'echo "Hello, World"'
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
echo "Hello, World"
```

- Initialize the git repository in the hello directory.
```powershell
PS C:\Users\leeyn\work\hello> git init
Initialized empty Git repository in C:/Users/leeyn/work/hello/.git/
```

- Check the status and act accordingly with the output of the executed command.
```powershell
PS C:\Users\leeyn\work\hello> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.sh

nothing added to commit but untracked files present (use "git add" to track)
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "first commit"
[master (root-commit) 4e1dfc2] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.sh
```

- Change the hello.sh content to the following:
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

echo "Hello, $1"
```

- Stage the changed file and commit the changes, the working tree should be clean.
```powershell
PS C:\Users\leeyn\work\hello> git add hello.sh
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
PS C:\Users\leeyn\work\hello> git commit -m "second commit"
[master e1cc968] second commit
 1 file changed, 3 insertions(+), 1 deletion(-)
```

- Modify the hello.sh file to include comments and stage it.
```powershell
PS C:\Users\leeyn\work\hello> cat .\hello.sh 
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

- Make two separate commits:
- The first commit should be for the comment in line 3.
```powershell
PS C:\Users\leeyn\work\hello> git add -p hello.sh
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
# Manual hunk edit mode -- see bottom for a quick guide.
diff --git a/hello.sh b/hello.sh
index 908e971..34290fb 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,5 @@
 #!/bin/bash

-echo "Hello, $1"
+# Default is "World"
+name=${1:-"World"}
+echo "Hello, $name"
\ No newline at end of file
(1/1) Stage this hunk [y,n,q,a,d,e,p,?]? e
PS C:\Users\leeyn\work\hello> git diff --staged
diff --git a/hello.sh b/hello.sh
index 908e971..a7ade22 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,3 @@
 #!/bin/bash

-echo "Hello, $1"
+# Default is "World"
PS C:\Users\leeyn\work\hello> git commit -m "comment on default value"
[master f0993d5] comment on default value
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- The second commit should include changes made to lines 4 and 5.
```powershell
PS C:\Users\leeyn\work\hello> git add hello.sh
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
PS C:\Users\leeyn\work\hello> git diff --staged
diff --git a/hello.sh b/hello.sh
index a7ade22..34290fb 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,5 @@
 #!/bin/bash

 # Default is "World"
+name=${1:-"World"}
+echo "Hello, $name"
\ No newline at end of file
PS C:\Users\leeyn\work\hello> git commit -m "initialise name and echo"
[master 08cb10a] initialise name and echo
 1 file changed, 2 insertions(+)
```
---

## History
- Show the history of the working directory.
```powershell
PS C:\Users\leeyn\work\hello> git log 
commit 08cb10ab36e02bb78d166a6a59cc90c7c25570ea (HEAD -> master)
Author: leeyn <leeyn.shun@gmail.com>
Date:   Wed Oct 9 09:49:39 2024 +0300

    initialise name and echo

commit f0993d5ed9b8c8a26f5b26ba6501784347f694c5
Author: leeyn <leeyn.shun@gmail.com>
Date:   Wed Oct 9 09:48:25 2024 +0300

    comment on default value

commit e1cc96809b04e64db37dd64e2e97c22a6d680fd4
Author: leeyn <leeyn.shun@gmail.com>
Date:   Wed Oct 9 09:36:58 2024 +0300

    second commit

commit 4e1dfc20daa1110efde6c8d7325fd21279c9ad7c
Author: leeyn <leeyn.shun@gmail.com>
Date:   Wed Oct 9 09:35:01 2024 +0300

    first commit
```

- Show One-Line History for a condensed view showing only commit hashes and messages.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline
08cb10a (HEAD -> master) initialise name and echo
f0993d5 comment on default value
e1cc968 second commit
4e1dfc2 first commit
```

- Controlled Entries:
    You need to customize the log output by specifying the number of entries or a time range. 
    Customize it to display the last 2 entries and to view the commits made within the last 5 minutes.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline -n 2
08cb10a (HEAD -> master) initialise name and echo
f0993d5 comment on default value
```

- Personalized Format:
       Show logs in a personalized format, including the commit hash, date, message, branch information, and author name, resembling * e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe]
```powershell
PS C:\Users\leeyn\work\hello> git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
* 08cb10a 2024-10-09 | initialise name and echo ( (HEAD -> master)) [leeyn]
* f0993d5 2024-10-09 | comment on default value () [leeyn]
* e1cc968 2024-10-09 | second commit () [leeyn]
* 4e1dfc2 2024-10-09 | first commit () [leeyn]
```
---

## Check it out
- Restore First Snapshot:
    Revert the working tree to its initial state, as captured in the first snapshot, 
    and then print the content of the hello.sh file.
```powershell
PS C:\Users\leeyn\work\hello> git reset --hard 4e1dfc2
HEAD is now at 4e1dfc2 first commit
PS C:\Users\leeyn\work\hello> cat hello.sh
echo "Hello, World"
```

- Restore Second Recent Snapshot:
    Revert the working tree to the second most recent snapshot and print the content of the hello.sh file.
```powershell
PS C:\Users\leeyn\work\hello> git reset --hard f0993d5
HEAD is now at f0993d5 comment on default value
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is "World"
```

- Return to Latest Version:
    Ensure that the working directory reflects the latest version of the hello.sh file present in the main branch, 
    without referring to specific commit hashes.
```powershell
PS C:\Users\leeyn\work\hello> git reflog
f0993d5 (HEAD -> master) HEAD@{0}: reset: moving to f0993d5
e1cc968 HEAD@{1}: reset: moving to e1cc968
4e1dfc2 HEAD@{2}: reset: moving to 4e1dfc2
08cb10a HEAD@{3}: commit: initialise name and echo
f0993d5 (HEAD -> master) HEAD@{4}: commit: comment on default value
e1cc968 HEAD@{5}: reset: moving to HEAD
e1cc968 HEAD@{6}: commit: second commit
4e1dfc2 HEAD@{7}: reset: moving to HEAD
4e1dfc2 HEAD@{8}: commit (initial): first commit
PS C:\Users\leeyn\work\hello> git reset --hard 08cb10a
HEAD is now at 08cb10a initialise name and echo
PS C:\Users\leeyn\work\hello> cat .\hello.sh
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```
---

## TAG me
- Referencing Current Version:
    Tag the current version of the repository as v1.
```powershell
PS C:\Users\leeyn\work\hello> git tag v1
```

- Tagging Previous Version:
    Tag the version immediately prior to the current version as v1-beta, 
    without relying on commit hashes to navigate through the history.
```powershell
PS C:\Users\leeyn\work\hello> git tag v1-beta v1^
```

- Navigating Tagged Versions:
    Move back and forth between the two tagged versions, v1 and v1-beta.
```powershell
PS C:\Users\leeyn\work\hello> git checkout v1-beta
Note: switching to 'v1-beta'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f0993d5 comment on default value
HEAD is now at f0993d5 comment on default value
PS C:\Users\leeyn\work\hello> git checkout v1
Previous HEAD position was f0993d5 comment on default value
HEAD is now at 08cb10a initialise name and echo
```

- Listing Tags:
    Display a list of all tags present in the repository to verify successful tagging.
```powershell
PS C:\Users\leeyn\work\hello> git tag
v1
v1-beta
```
---

## Changed your mind?
- Reverting Changes:
    Modify the latest version of the file with unwanted comments, 
    then revert it back to its original state before staging using a Git command.
```console
PS C:\Users\leeyn\work\hello> cat .\hello.sh
#!/bin/bash

# This is a bad comment. We want to revert it.
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git checkout -- hello.sh
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

- Staging and Cleaning:
    Introduce unwanted changes to the file, stage them, then clean the staging area to discard the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git status
HEAD detached at v1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   hello.sh
PS C:\Users\leeyn\work\hello> git restore --staged hello.sh
PS C:\Users\leeyn\work\hello> git restore hello.sh
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
```

- Committing and Reverting:
    Add the following unwanted changes again, stage the file, commit the changes, 
    then revert them back to their original state.
```powershell
#!/bin/bash

# This is an unwanted but committed change
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "commiting unwanted change"
[detached HEAD 9ed87ca] commiting unwanted change
 1 file changed, 2 insertions(+), 1 deletion(-)
 PS C:\Users\leeyn\work\hello> git log --oneline
9ed87ca (HEAD) commiting unwanted change
08cb10a (tag: v1, master) initialise name and echo
f0993d5 (tag: v1-beta) comment on default value
e1cc968 second commit
4e1dfc2 first commit
PS C:\Users\leeyn\work\hello> git revert HEAD
[detached HEAD b74801d] Revert "commiting unwanted change"
 1 file changed, 1 insertion(+), 2 deletions(-)
 PS C:\Users\leeyn\work\hello> git log --oneline
b74801d (HEAD) Revert "commiting unwanted change"
9ed87ca commiting unwanted change
08cb10a (tag: v1, master) initialise name and echo
f0993d5 (tag: v1-beta) comment on default value
e1cc968 second commit
4e1dfc2 first commit
```

- Tagging and Removing Commits:
    Tag the latest commit with oops, then remove commits made after the v1 version. 
    Ensure that the HEAD points to v1.
```powershell
PS C:\Users\leeyn\work\hello> git tag oops
PS C:\Users\leeyn\work\hello> git reset --hard v1
HEAD is now at 08cb10a initialise name and echo
PS C:\Users\leeyn\work\hello> git log --oneline
08cb10a (HEAD, tag: v1, master) initialise name and echo
f0993d5 (tag: v1-beta) comment on default value
e1cc968 second commit
4e1dfc2 first commit
```

- Displaying Logs with Deleted Commits:
    Show the logs with the deleted commits displayed, particularly focusing on the commit tagged oops.
    08cb10a (HEAD, tag: v1, master) HEAD@{0}: reset: moving to v1
```powershell
PS C:\Users\leeyn\work\hello> git reflog
08cb10a (HEAD, tag: v1, master) HEAD@{0}: reset: moving to v1
b74801d (tag: oops) HEAD@{1}: revert: Revert "commiting unwanted change"
9ed87ca HEAD@{2}: commit: commiting unwanted change
08cb10a (HEAD, tag: v1, master) HEAD@{3}: checkout: moving from f0993d5ed9b8c8a26f5b26ba6501784347f694c5 to v1
f0993d5 (tag: v1-beta) HEAD@{4}: checkout: moving from master to v1-beta
08cb10a (HEAD, tag: v1, master) HEAD@{5}: checkout: moving from f0993d5ed9b8c8a26f5b26ba6501784347f694c5 to master
f0993d5 (tag: v1-beta) HEAD@{6}: checkout: moving from master to v1-beta
08cb10a (HEAD, tag: v1, master) HEAD@{7}: reset: moving to 08cb10a
f0993d5 (tag: v1-beta) HEAD@{8}: reset: moving to f0993d5
08cb10a (HEAD, tag: v1, master) HEAD@{9}: reset: moving to 08cb10a
f0993d5 (tag: v1-beta) HEAD@{10}: reset: moving to f0993d5
e1cc968 HEAD@{11}: reset: moving to e1cc968
4e1dfc2 HEAD@{12}: reset: moving to 4e1dfc2
08cb10a (HEAD, tag: v1, master) HEAD@{13}: commit: initialise name and echo
f0993d5 (tag: v1-beta) HEAD@{14}: commit: comment on default value
e1cc968 HEAD@{15}: reset: moving to HEAD
e1cc968 HEAD@{16}: commit: second commit
4e1dfc2 HEAD@{17}: reset: moving to HEAD
4e1dfc2 HEAD@{18}: commit (initial): first commit
```

- Cleaning Unreferenced Commits:
    Ensure that unreferenced commits are deleted from the history, 
    meaning there should be no logs for these deleted commits.
```powershell
PS C:\Users\leeyn\work\hello> git reflog expire --expire=now --all
PS C:\Users\leeyn\work\hello> git gc --prune=now
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 12 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (12/12), done.
Total 12 (delta 0), reused 12 (delta 0), pack-reused 0 (from 0)
PS C:\Users\leeyn\work\hello> git reflog
PS C:\Users\leeyn\work\hello> git log --oneline
08cb10a (HEAD, tag: v1, master) initialise name and echo
f0993d5 (tag: v1-beta) comment on default value
e1cc968 second commit
4e1dfc2 first commit
```

- Author Information:
    Add an author comment to the file and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is World
# Author: Jim Weirich
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "adding author indo"
[detached HEAD 6190ecc] adding author indo
 1 file changed, 3 insertions(+), 1 deletion(-)
```

- Oops the author email was forgotten, update the file to include the email without making a new commit, 
    but include the change in the last commit.
```powershell
PS C:\Users\leeyn\work\hello> git add .\hello.sh
PS C:\Users\leeyn\work\hello> git commit --amend --no-edit
[detached HEAD 85b6663] adding author indo
 Date: Wed Oct 9 12:22:46 2024 +0300
 1 file changed, 4 insertions(+), 1 deletion(-)
PS C:\Users\leeyn\work\hello> git show
commit 85b666376506bcd499215d67ce985892bf45789e (HEAD)
Author: leeyn <leeyn.shun@gmail.com>
Date:   Wed Oct 9 12:22:46 2024 +0300

    adding author indo

diff --git a/hello.sh b/hello.sh
index 34290fb..1e2bbb4 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,5 +1,8 @@
 #!/bin/bash

-# Default is "World"
+# Default is World
+# Author: Jim Weirich
+# Email: jim.weirich@hello.world
 name=${1:-"World"}
+
 echo "Hello, $name"
\ No newline at end of file
```
---

## Move it
- Moving hello.sh:
    Using Git commands, move the program hello.sh into a lib/ directory, and then commit the move.
```powershell
PS C:\Users\leeyn\work\hello> mkdir lib


    Directory: C:\Users\leeyn\work\hello


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         9/10/2024   1:02 pm                lib


PS C:\Users\leeyn\work\hello> git mv hello.sh lib/
PS C:\Users\leeyn\work\hello> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    hello.sh -> lib/hello.sh
```

- Create a Makefile in the root directory of the repository with the provided content 
    and commit it to the repository.
```powershell
PS C:\Users\leeyn\work\hello> cat Makefile
TARGET="lib/hello.sh"

run:
        bash ${TARGET}
PS C:\Users\leeyn\work\hello> git add Makefile
PS C:\Users\leeyn\work\hello> git commit -m "create Makefile"
[master 458356d] create Makefile
 2 files changed, 4 insertions(+)
 create mode 100644 Makefile
 rename hello.sh => lib/hello.sh (100%)
```
---

## blobs, trees and commits
- Exploring .git/ Directory:
    Navigate to the .git/ directory in your project and examine its contents.You will have to explain the purpose of each subdirectory, including objects/, config, refs, and HEAD in the audit.
```powershell
PS C:\Users\leeyn\work\hello\.git> ls


    Directory: C:\Users\leeyn\work\hello\.git


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         9/10/2024   9:30 am                hooks
d-----         9/10/2024  12:18 pm                info
d-----         9/10/2024  12:18 pm                logs
d-----         9/10/2024   1:11 pm                objects
d-----         9/10/2024   9:30 am                refs
-a----         9/10/2024   1:11 pm             16 COMMIT_EDITMSG
-a----         9/10/2024   9:30 am            130 config
-a----         9/10/2024   9:30 am             73 description
-a----         9/10/2024  12:59 pm             23 HEAD
-a----         9/10/2024   1:11 pm            245 index
-a----         9/10/2024  12:59 pm             41 ORIG_HEAD
-a----         9/10/2024  12:18 pm            218 packed-refs


```

- Latest Object Hash:
    Find the latest object hash within the .git/objects/ directory using Git commands and print the type and content of this object using Git commands.
```powershell
PS C:\Users\leeyn\work\hello\.git> git rev-list --objects --all | Select-Object -First 1   
458356d3d75dfc014cebf7b3a9fcf6849be5535a
PS C:\Users\leeyn\work\hello\.git> git cat-file -p 458356d3d75dfc014cebf7b3a9fcf6849be5535a
tree 6da6e246e6bc2791f7885056882dddb783b35828
parent 85b666376506bcd499215d67ce985892bf45789e
author leeyn <leeyn.shun@gmail.com> 1728468668 +0300
committer leeyn <leeyn.shun@gmail.com> 1728468668 +0300

create Makefile
```

- Dumping Directory Tree:
    Use Git commands to dump the directory tree referenced by this commit.
```powershell
PS C:\Users\leeyn\work\hello\.git> git ls-tree 458356d3d75dfc014cebf7b3a9fcf6849be5535a
100644 blob ea5f53171f00e91a8384b7854278b09bd0669373    Makefile
040000 tree 7d2582ba983e1885b25204260b4c53cff53f9a9e    lib
```

- Dump the contents of the lib/ directory and the hello.sh file using Git commands
```powershell
PS C:\Users\leeyn\work\hello\.git> git ls-tree -r 458356d3d75dfc014cebf7b3a9fcf6849be5535a
100644 blob ea5f53171f00e91a8384b7854278b09bd0669373    Makefile
100644 blob 1e2bbb4db1bc91a674d343dd89c3de4de7d32d60    lib/hello.sh
PS C:\Users\leeyn\work\hello\.git> git show 1e2bbb4db1bc91a674d343dd89c3de4de7d32d60 
#!/bin/bash

# Default is World
# Author: Jim Weirich
# Email: jim.weirich@hello.world
name=${1:-"World"}

echo "Hello, $name"
```
---

## Branching
- Create a local branch named greet and switch to it.
```powershell
PS C:\Users\leeyn\work\hello> git checkout -b greet
Switched to a new branch 'greet'
```

- In the lib directory, create a new file named greeter.sh and add the provided code to it. Commit these changes.
```powershell
PS C:\Users\leeyn\work\hello> code lib\greeter.sh
PS C:\Users\leeyn\work\hello> cat lib\greeter.sh
#!/bin/bash

Greeter() {
    who="$1"
    echo "Hello, $who"
}
PS C:\Users\leeyn\work\hello> git add lib\greeter.sh
warning: in the working copy of 'lib/greeter.sh', LF will be replaced by CRLF the next time Git touches it
PS C:\Users\leeyn\work\hello> git commit -m "adding greeter.sh"
[greet d5fb316] adding greeter.sh
 1 file changed, 6 insertions(+)
 create mode 100644 lib/greeter.sh
```

- Update the lib/hello.sh file by adding the content below, stage and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat lib\hello.sh
#!/bin/bash

source lib/greeter.sh

name="$1"
if [ -z "$name" ]; then
    name="World"
fi

Greeter "$name"
PS C:\Users\leeyn\work\hello> git add lib\hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "modify hello.sh to use greeter"
[greet a51b1ec] modify hello.sh to use greeter
 1 file changed, 7 insertions(+), 5 deletions(-)
```

- Update the Makefile with the following comment and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat Makefile
# Ensure it runs the updated lib/hello.sh file
TARGET="lib/hello.sh"

run:
        bash ${TARGET}
PS C:\Users\leeyn\work\hello> git add Makefile
PS C:\Users\leeyn\work\hello> git commit -m "add comments in Makefile"
[greet f0324ac] add comments in Makefile
 1 file changed, 1 insertion(+)
```

- Switch back to the main branch, compare and show the differences between the main 
    and greet branches for Makefile, hello.sh, and greeter.sh files.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Switched to branch 'master'
PS C:\Users\leeyn\work\hello> git diff greet -- Makefile
diff --git a/Makefile b/Makefile
index 76d2148..ea5f531 100644
--- a/Makefile
+++ b/Makefile
@@ -1,4 +1,3 @@
-# Ensure it runs the updated lib/hello.sh file
 TARGET="lib/hello.sh"

 run:
PS C:\Users\leeyn\work\hello> git diff greet -- lib\hello.sh
diff --git a/lib/hello.sh b/lib/hello.sh
index 56a4589..1e2bbb4 100644
--- a/lib/hello.sh
+++ b/lib/hello.sh
@@ -1,10 +1,8 @@
 #!/bin/bash

-source lib/greeter.sh
+# Default is World
+# Author: Jim Weirich
+# Email: jim.weirich@hello.world
+name=${1:-"World"}

-name="$1"
-if [ -z "$name" ]; then
-    name="World"
-fi
-
-Greeter "$name"
PS C:\Users\leeyn\work\hello> git diff greet -- lib\greeter.sh
diff --git a/lib/greeter.sh b/lib/greeter.sh
deleted file mode 100644
index c5ff539..0000000
--- a/lib/greeter.sh
+++ /dev/null
@@ -1,6 +0,0 @@
-#!/bin/bash
-
-Greeter() {
-    who="$1"
-    echo "Hello, $who"
-}
\ No newline at end of file
```

- Generate a README.md file for the project with the provided content. Commit this file.
```powershell
PS C:\Users\leeyn\work\hello> git add README.md
PS C:\Users\leeyn\work\hello> git commit -m "adding README.md"
[master a3b5132] adding README.md
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

- Draw a commit tree diagram illustrating the diverging changes between all branches to demonstrate the branch history.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
* a3b5132 (HEAD -> master) adding README.md
| * f0324ac (greet) add comments in Makefile
| * a51b1ec modify hello.sh to use greeter
| * d5fb316 adding greeter.sh
|/
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```
---

## Conflicts, merging and rebasing
- Merge Main into Greet Branch:
    Start by merging the changes from the main branch into the greet branch.
```powershell
PS C:\Users\leeyn\work\hello> git checkout greet
Switched to branch 'greet'
PS C:\Users\leeyn\work\hello> git merge master
Merge made by the 'ort' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

- Switch to main branch and make the changes below to the hello.sh file, save and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat lib\hello.sh    
#!/bin/bash

echo "What's your name"
read my_name

echo "Hello, $my_name"
PS C:\Users\leeyn\work\hello> git add lib\hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "read input for hello"
[master 2fe3013] read input for hello
 1 file changed, 3 insertions(+), 5 deletions(-)
```

- Merging Main into Greet Branch (Conflict):
    Attempt to merge the main branch into greet. Bingooo! There you have it, a conflict.
    Resolve the conflict (manually or using graphical merge tools), accept changes from main branch, then commit the conflict resolution.
```powershell
PS C:\Users\leeyn\work\hello> git checkout greet
Switched to branch 'greet'
PS C:\Users\leeyn\work\hello> git merge master
Auto-merging lib/hello.sh
CONFLICT (content): Merge conflict in lib/hello.sh
Automatic merge failed; fix conflicts and then commit the result.
PS C:\Users\leeyn\work\hello> git add lib/hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "resolve merge conflict between greet and master"
[greet 3bf469b] resolve merge conflict between greet and master
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
*   3bf469b (HEAD -> greet) resolve merge conflict between greet and master
|\
| * 2fe3013 (master) read input for hello
* | f676206 Merge branch 'master' into greet
|\|
| * a3b5132 adding README.md
* | f0324ac add comments in Makefile
* | a51b1ec modify hello.sh to use greeter
* | d5fb316 adding greeter.sh
|/
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Rebasing Greet Branch:
    Go back to the point before the initial merge between main and greet.
    Rebase the greet branch on top of the latest changes in the main branch.
```powershell
PS C:\Users\leeyn\work\hello> git reset --hard f0324ac
HEAD is now at f0324ac add comments in Makefile
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
* a3b5132 (master) adding README.md
| * f0324ac (HEAD -> greet) add comments in Makefile
| * a51b1ec modify hello.sh to use greeter
| * d5fb316 adding greeter.sh
|/  
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
PS C:\Users\leeyn\work\hello> git rebase master
Successfully rebased and updated refs/heads/greet.
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
* a2f0608 (HEAD -> greet) add comments in Makefile
* f6424e5 modify hello.sh to use greeter
* 000d473 adding greeter.sh
* a3b5132 (master) adding README.md
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Merging Greet into Main:
    Merge the changes from the greet branch into the main branch.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Switched to branch 'master'
PS C:\Users\leeyn\work\hello> git merge greet
Updating a3b5132..a2f0608
Fast-forward
 Makefile       |  1 +
 lib/greeter.sh |  6 ++++++
 lib/hello.sh   | 12 +++++++-----
 3 files changed, 14 insertions(+), 5 deletions(-)
 create mode 100644 lib/greeter.sh
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
* a2f0608 (HEAD -> master, greet) add comments in Makefile
* f6424e5 modify hello.sh to use greeter
* 000d473 adding greeter.sh
* a3b5132 adding README.md
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Understanding Fast-Forwarding and Differences:
    Explain fast-forwarding and the difference between merging and rebasing.

    Fast-fowarding: When there are no new commits on 'A' branch, while there are new commits on 'B'. (No diverting branches)
    Git simply moves the 'A' branch pointer to the latest commit of 'B'

    Merging takes the changes from one branch and integrate them into another branch.
    The history/ commits of both branches will be preserve.

    Rebasing combines a sequence of commits into a new base commit.
    It rewrites another branch's commit history with the current one.

| Feature | Merging | Rebasing |
| ------- | ------- | -------- |
| Commit History | Non-Linear; shows diverging branches | Linear; integrates changes on top |
| Merge Commit | Create a merge commit | No merge commit created |
| conflict Resolution | Resolves conflicts once at the merge | Resolves conflicts at each commit |
| Best Used For | Integrating changes from different branches | Keep a clean project history |
| Collaboration | Preserves original history, good for teamwork | Suitable for local feature branches before merging |
---

## Local and remote repositories
- In the work/ directory, make a clone of the repository hello as cloned_hello. (Do not use copy command)
```powershell
PS C:\Users\leeyn\work> git clone hello cloned_hello
Cloning into 'cloned_hello'...
done.
```

- Show the logs for the cloned repository.
```powershell
PS C:\Users\leeyn\work> cd .\cloned_hello\
PS C:\Users\leeyn\work\cloned_hello> git log --oneline --all --graph
* a2f0608 (HEAD -> master, origin/master, origin/greet, origin/HEAD) add comments in Makefile
* f6424e5 modify hello.sh to use greeter
* 000d473 adding greeter.sh
* a3b5132 adding README.md
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Display the name of the remote repository and provide more information about it.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git remote
origin
PS C:\Users\leeyn\work\cloned_hello> git remote show origin
* remote origin
  Fetch URL: C:/Users/leeyn/work/hello
  Push  URL: C:/Users/leeyn/work/hello
  HEAD branch: master
  Remote branches:
    greet  tracked
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```

- List all remote and local branches in the cloned_hello repository.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git branch --all
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/greet
  remotes/origin/master
```

- Make changes to the original repository, update the README.md file with the provided content, and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat README.md
This is the Hello World example from the git project.
(changed in the original)
PS C:\Users\leeyn\work\hello> git add README.md
PS C:\Users\leeyn\work\hello> git commit -m "changed in orginal"
[master a806bdc] changed in orginal
 1 file changed, 2 insertions(+), 1 deletion(-)
```

- Inside the cloned repository (cloned_hello), fetch the changes from the remote repository and display the logs. Ensure that commits from the hello repository are included in the logs.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git fetch origin
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 358 bytes | 18.00 KiB/s, done.
From C:/Users/leeyn/work/hello
   a2f0608..a806bdc  master     -> origin/master
PS C:\Users\leeyn\work\cloned_hello> git log --oneline --all --graph
* a806bdc (origin/master, origin/HEAD) changed in orginal
* a2f0608 (HEAD -> master, origin/greet) add comments in Makefile
* f6424e5 modify hello.sh to use greeter
* 000d473 adding greeter.sh
* a3b5132 adding README.md
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Merge the changes from the remote main branch into the local main branch.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git merge origin\master
merge: origin\master - not something we can merge
PS C:\Users\leeyn\work\cloned_hello> git merge origin/master
Updating a2f0608..a806bdc
Fast-forward
 README.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

- Add a local branch named greet tracking the remote origin/greet branch.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git checkout -b greet origin/greet
branch 'greet' set up to track 'origin/greet'.
Switched to a new branch 'greet'
PS C:\Users\leeyn\work\cloned_hello> git log --oneline --all --graph                          
* a806bdc (origin/master, origin/HEAD, master) changed in orginal
* a2f0608 (HEAD -> greet, origin/greet) add comments in Makefile
* f6424e5 modify hello.sh to use greeter
* 000d473 adding greeter.sh
* a3b5132 adding README.md
* 458356d create Makefile
* 85b6663 adding author indo
* 08cb10a (tag: v1) initialise name and echo
* f0993d5 (tag: v1-beta) comment on default value
* e1cc968 second commit
* 4e1dfc2 first commit
```

- Add a remote to your Git repository and push the main and greet branches to the remote.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git remote add gritLab https://01.gritlab.ax/git/ylee/git
PS C:\Users\leeyn\work\cloned_hello> git remote -v
gritLab https://01.gritlab.ax/git/ylee/git (fetch)
gritLab https://01.gritlab.ax/git/ylee/git (push)
origin  C:/Users/leeyn/work/hello (fetch)
origin  C:/Users/leeyn/work/hello (push)
PS C:\Users\leeyn\work\cloned_hello> git push -u gritLab master
Enumerating objects: 35, done.
Counting objects: 100% (35/35), done.
Delta compression using up to 12 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (35/35), 3.23 KiB | 254.00 KiB/s, done.
Total 35 (delta 3), reused 12 (delta 0), pack-reused 0 (from 0)
remote: . Processing 1 references
remote: Processed 1 references in total
To https://01.gritlab.ax/git/ylee/git
 * [new branch]      master -> master
branch 'master' set up to track 'gritLab/master'.
PS C:\Users\leeyn\work\cloned_hello> git push -u gritLab greet 
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a new pull request for 'greet':
remote:   https://01.gritlab.ax/git/ylee/git/compare/master...greet
remote:
remote: . Processing 1 references
remote: Processed 1 references in total
To https://01.gritlab.ax/git/ylee/git
 * [new branch]      greet -> greet
branch 'greet' set up to track 'gritLab/greet'.
```

### "What is the single git command equivalent to what you did before to bring changes from remote to local main branch?"
git pull remote [local-branch]

## Bare repositories
- What is a bare repository and why is it needed?
    A bare repository is a git reporsitory without the working directory. It contains the version control and files required to track changes, similar to the content of the .git directory. It is usually stored in a remote location and is useful for collaboration among multiple developers.

- Create a bare repository named hello.git from the existing hello repository.
```powershell
PS C:\Users\leeyn\work> git clone --bare hello hello.git
Cloning into bare repository 'hello.git'...
done.
```

- Add the bare hello.git repository as a remote to the original repository hello.
```powershell
PS C:\Users\leeyn\work\hello> git remote add bareHello ../hello.git
PS C:\Users\leeyn\work\hello> git remote -v
bareHello       ../hello.git (fetch)
bareHello       ../hello.git (push)
```

- Change the README.md file in the original repository with the provided content:
```powershell
PS C:\Users\leeyn\work\hello> cat README.md   
This is the Hello World example from the git project.
(Changed in the original and pushed to shared)
```

- Commit the changes and push them to the shared repository.
```powershell
PS C:\Users\leeyn\work\hello> git add README.md
PS C:\Users\leeyn\work\hello> git commit -m "shared README"
[master 0762916] shared README
 1 file changed, 1 insertion(+), 1 deletion(-)
 PS C:\Users\leeyn\work\hello> git push --set-upstream bareHello master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 396 bytes | 396.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To ../hello.git
   a806bdc..0762916  master -> master
branch 'master' set up to track 'bareHello/master'.
PS C:\Users\leeyn\work\hello> git push bareHello
Everything up-to-date
```

- Switch to the cloned repository cloned_hello and pull down the changes just pushed to the shared repository.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git remote add bareHello ../hello.git
PS C:\Users\leeyn\work\cloned_hello> git pull bareHello master
From ../hello
 * branch            master     -> FETCH_HEAD
Updating a806bdc..0762916
Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
 PS C:\Users\leeyn\work\cloned_hello> cat README.md
This is the Hello World example from the git project.
(Changed in the original and pushed to shared)
```
---
