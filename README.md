# git

## Setting Up Git
- Configure Git with your username and email address.
```powershell
PS C:\Users\leeyn\work> git config --global -l
user.name=leeyn
user.email=leeyn.shun@gmail.com
credential.https://01.gritlab.ax.provider=generic
```
---

## Git commits to commit
- Within the work directory, establish a subdirectory named hello. 
```powershell
PS C:\Users\leeyn\work> mkdir hello


    Directory: C:\Users\leeyn\work


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        13/10/2024  11:02 am                hello


PS C:\Users\leeyn\work> cd hello
PS C:\Users\leeyn\work\hello> 
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
[master (root-commit) 2c4b412] first commit
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
[master d04fdf6] second commit
 1 file changed, 3 insertions(+), 1 deletion(-)
PS C:\Users\leeyn\work\hello> git status
On branch master
nothing to commit, working tree clean
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
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
diff --git a/hello.sh b/hello.sh
index c6206bd..34290fb 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,5 @@
 #!/bin/bash

-echo "Hello, $1"
\ No newline at end of file
+# Default is "World"
+name=${1:-"World"}
+echo "Hello, $name"
\ No newline at end of file
(1/1) Stage this hunk [y,n,q,a,d,e,p,?]? e

PS C:\Users\leeyn\work\hello> git diff --staged
diff --git a/hello.sh b/hello.sh
index c6206bd..a7ade22 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,3 @@
 #!/bin/bash

-echo "Hello, $1"
\ No newline at end of file
+# Default is "World"
PS C:\Users\leeyn\work\hello> git commit -m "comment on default value" 
[master bc714b2] comment on default value
 1 file changed, 1 insertion(+), 1 deletion(-)
PS C:\Users\leeyn\work\hello> 
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
[master 1d089b5] initialise name and echo
 1 file changed, 2 insertions(+)
```
---

## History
- Show the history of the working directory.
```powershell
PS C:\Users\leeyn\work\hello> git log
commit 1d089b57a26ce1e7cdb1a7ae77e2aecd2d9efd23 (HEAD -> master)
Author: leeyn <leeyn.shun@gmail.com>
Date:   Sun Oct 13 11:11:42 2024 +0300

    initialise name and echo

commit bc714b2c7fa71fe5ea2dfa22678c5262c686ccf2
Author: leeyn <leeyn.shun@gmail.com>
Date:   Sun Oct 13 11:09:09 2024 +0300

    comment on default value

commit d04fdf62716557856161cea60f5f7cbbd9e7ab84
Author: leeyn <leeyn.shun@gmail.com>
Date:   Sun Oct 13 11:07:16 2024 +0300

    second commit

commit 2c4b412fff0e0e11f91c1bbbb8f9ba2f8a7dfdfa
Author: leeyn <leeyn.shun@gmail.com>
Date:   Sun Oct 13 11:05:49 2024 +0300

    first commit
```

- Show One-Line History for a condensed view showing only commit hashes and messages.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline
1d089b5 (HEAD -> master) initialise name and echo
bc714b2 comment on default value
d04fdf6 second commit
2c4b412 first commit
```

- Controlled Entries:
    You need to customize the log output by specifying the number of entries or a time range. 
    Customize it to display the last 2 entries and to view the commits made within the last 5 minutes.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline --since="5 minutes ago" -n 2
1d089b5 (HEAD -> master) initialise name and echo
bc714b2 comment on default value
```

- Personalized Format:
       Show logs in a personalized format, including the commit hash, date, message, branch information, and author name, resembling * e4e3645 2023-06-10 | Added a comment (HEAD -> main) [John Doe]
```powershell
PS C:\Users\leeyn\work\hello> git log --pretty=format:"* %h %ad | %s (%d) [%an]" --date=short
* 1d089b5 2024-10-13 | initialise name and echo ( (HEAD -> master)) [leeyn]
* bc714b2 2024-10-13 | comment on default value () [leeyn]
* d04fdf6 2024-10-13 | second commit () [leeyn]
* 2c4b412 2024-10-13 | first commit () [leeyn]
```
---

## Check it out
- Restore First Snapshot:
    Revert the working tree to its initial state, as captured in the first snapshot, 
    and then print the content of the hello.sh file.
```powershell
PS C:\Users\leeyn\work\hello> git checkout 2c4b412
Note: switching to '2c4b412'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 2c4b412 first commit
PS C:\Users\leeyn\work\hello> cat hello.sh
echo "Hello, World"
```

- Restore Second Recent Snapshot:
    Revert the working tree to the second most recent snapshot and print the content of the hello.sh file.
```powershell
PS C:\Users\leeyn\work\hello> git checkout bc714b2
Previous HEAD position was 2c4b412 first commit
HEAD is now at bc714b2 comment on default value
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is "World"
```

- Return to Latest Version:
    Ensure that the working directory reflects the latest version of the hello.sh file present in the main branch, 
    without referring to specific commit hashes.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Previous HEAD position was bc714b2 comment on default value
Switched to branch 'master'
PS C:\Users\leeyn\work\hello> cat hello.sh
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
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# This is a bad comment. We want to revert it.
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git restore -- hello.sh
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

# This is an unwanted but staged comment
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git status
HEAD detached at v1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   hello.sh

PS C:\Users\leeyn\work\hello> git restore --stage hello.sh
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
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# This is an unwanted but committed change
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git add hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "commiting unwanted changes"
Revert "commiting unwanted changes"
[detached HEAD 0f50b78] commiting unwanted changes
 1 file changed, 2 insertions(+), 1 deletion(-)
PS C:\Users\leeyn\work\hello> git log --oneline
0f50b78 (HEAD) commiting unwanted changes
1d089b5 (tag: v1, master) initialise name and echo
bc714b2 (tag: v1-beta) comment on default value
d04fdf6 second commit
2c4b412 first commit
PS C:\Users\leeyn\work\hello> git revert HEAD
[detached HEAD 37b0847] Revert "commiting unwanted changes"
 1 file changed, 1 insertion(+), 2 deletions(-)
PS C:\Users\leeyn\work\hello> git log --oneline
37b0847 (HEAD) Revert "commiting unwanted changes"
0f50b78 commiting unwanted changes
1d089b5 (tag: v1, master) initialise name and echo
bc714b2 (tag: v1-beta) comment on default value
d04fdf6 second commit
2c4b412 first commit
```

- Tagging and Removing Commits:
    Tag the latest commit with oops, then remove commits made after the v1 version. 
    Ensure that the HEAD points to v1.
```powershell
PS C:\Users\leeyn\work\hello> git tag oops
PS C:\Users\leeyn\work\hello> git reset --hard v1
HEAD is now at 1d089b5 initialise name and echo
PS C:\Users\leeyn\work\hello> git log --oneline
1d089b5 (HEAD, tag: v1, master) initialise name and echo
bc714b2 (tag: v1-beta) comment on default value
d04fdf6 second commit
2c4b412 first commit
```

- Displaying Logs with Deleted Commits:
    Show the logs with the deleted commits displayed, particularly focusing on the commit tagged oops.
```powershell
PS C:\Users\leeyn\work\hello> git log oops --oneline
37b0847 (tag: oops) Revert "commiting unwanted changes"
0f50b78 commiting unwanted changes
1d089b5 (HEAD, tag: v1, master) initialise name and echo
bc714b2 (tag: v1-beta) comment on default value
d04fdf6 second commit
2c4b412 first commit
```

- Cleaning Unreferenced Commits:
    Ensure that unreferenced commits are deleted from the history, 
    meaning there should be no logs for these deleted commits.
```powershell
PS C:\Users\leeyn\work\hello> git reflog expire --expire-unreachable=now --all
PS C:\Users\leeyn\work\hello> git gc --prune=now
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 12 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (16/16), done.
Total 16 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
PS C:\Users\leeyn\work\hello> git reflog        
1d089b5 (HEAD, tag: v1, master) HEAD@{0}: reset: moving to v1
37b0847 (tag: oops) HEAD@{1}: revert: Revert "commiting unwanted changes"
0f50b78 HEAD@{2}: commit: commiting unwanted changes
1d089b5 (HEAD, tag: v1, master) HEAD@{3}: checkout: moving from bc714b2c7fa71fe5ea2dfa22678c5262c686ccf2 to v1
bc714b2 (tag: v1-beta) HEAD@{4}: checkout: moving from master to v1-beta
1d089b5 (HEAD, tag: v1, master) HEAD@{5}: checkout: moving from bc714b2c7fa71fe5ea2dfa22678c5262c686ccf2 to master
bc714b2 (tag: v1-beta) HEAD@{6}: checkout: moving from 2c4b412fff0e0e11f91c1bbbb8f9ba2f8a7dfdfa to bc714b2
2c4b412 HEAD@{7}: checkout: moving from master to 2c4b412
1d089b5 (HEAD, tag: v1, master) HEAD@{8}: commit: initialise name and echo
bc714b2 (tag: v1-beta) HEAD@{9}: commit: comment on default value
d04fdf6 HEAD@{10}: commit: second commit
2c4b412 HEAD@{11}: commit (initial): first commit

PS C:\Users\leeyn\work\hello> git tag -d oops
Deleted tag 'oops' (was 37b0847)
PS C:\Users\leeyn\work\hello> git reflog expire --expire-unreachable=now --all
PS C:\Users\leeyn\work\hello> git gc --prune=now
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 12 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (12/12), done.
Total 12 (delta 0), reused 12 (delta 0), pack-reused 0 (from 0)
PS C:\Users\leeyn\work\hello> git reflog
1d089b5 (HEAD, tag: v1, master) HEAD@{0}: checkout: moving from bc714b2c7fa71fe5ea2dfa22678c5262c686ccf2 to v1
bc714b2 (tag: v1-beta) HEAD@{1}: checkout: moving from master to v1-beta
1d089b5 (HEAD, tag: v1, master) HEAD@{2}: checkout: moving from bc714b2c7fa71fe5ea2dfa22678c5262c686ccf2 to master
bc714b2 (tag: v1-beta) HEAD@{3}: checkout: moving from 2c4b412fff0e0e11f91c1bbbb8f9ba2f8a7dfdfa to bc714b2
2c4b412 HEAD@{4}: checkout: moving from master to 2c4b412
1d089b5 (HEAD, tag: v1, master) HEAD@{5}: commit: initialise name and echo
bc714b2 (tag: v1-beta) HEAD@{6}: commit: comment on default value
d04fdf6 HEAD@{7}: commit: second commit
2c4b412 HEAD@{8}: commit (initial): first commit
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
PS C:\Users\leeyn\work\hello> git commit -m "adding author info"
[detached HEAD 1aa0d3d] adding author info
 1 file changed, 3 insertions(+), 1 deletion(-)
```

- Oops the author email was forgotten, update the file to include the email without making a new commit, 
    but include the change in the last commit.
```powershell
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

# Default is World
# Author: Jim Weirich <jim.weirich@hello.world>
name=${1:-"World"}

echo "Hello, $name"
PS C:\Users\leeyn\work\hello> git commit --amend --no-edit
[detached HEAD 005f9d9] adding author info
 Date: Sun Oct 13 11:57:55 2024 +0300
 1 file changed, 3 insertions(+), 1 deletion(-)
 PS C:\Users\leeyn\work\hello> git show
commit 005f9d92b247c360057f9215e90113668728c4be (HEAD, master)
Author: leeyn <leeyn.shun@gmail.com>
Date:   Sun Oct 13 11:57:55 2024 +0300

    adding author info

diff --git a/hello.sh b/hello.sh
index 34290fb..524792e 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,5 +1,7 @@
 #!/bin/bash

-# Default is "World"
+# Default is World
+# Author: Jim Weirich <jim.weirich@hello.world>
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
d-----        13/10/2024  12:06 pm                lib


PS C:\Users\leeyn\work\hello> git mv hello.sh lib/
PS C:\Users\leeyn\work\hello> git add lib/hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "moved hello.sh to lib"
[detached HEAD 84d6ad2] moved hello.sh to lib
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename hello.sh => lib/hello.sh (100%)
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
[master f539aa9] create Makefile
 1 file changed, 4 insertions(+)
 create mode 100644 Makefile
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
d-----        13/10/2024  11:05 am                hooks
d-----        13/10/2024  11:54 am                info
d-----        13/10/2024  11:54 am                logs
d-----        13/10/2024  12:09 pm                objects
d-----        13/10/2024  11:05 am                refs
-a----        13/10/2024  12:09 pm             16 COMMIT_EDITMSG
-a----        13/10/2024  11:05 am            130 config
-a----        13/10/2024  11:05 am             73 description
-a----        13/10/2024  12:08 pm             23 HEAD
-a----        13/10/2024  12:09 pm            245 index
-a----        13/10/2024  11:34 am             41 ORIG_HEAD
-a----        13/10/2024  11:54 am            218 packed-refs


```

- Latest Object Hash:
    Find the latest object hash within the .git/objects/ directory using Git commands and print the type and content of this object using Git commands.
```powershell
PS C:\Users\leeyn\work\hello\.git> git rev-list --objects --all | Select-Object -First 1 
f539aa9078557fafeaea1952e94bde778ccd3812
PS C:\Users\leeyn\work\hello\.git> git cat-file -t f539aa9078557fafeaea1952e94bde778ccd3812
commit
PS C:\Users\leeyn\work\hello\.git> git cat-file -p f539aa9078557fafeaea1952e94bde778ccd3812
tree 1b63fb93aa22cdc309117f7f52878c6d3676c154
parent 84d6ad2c8fdb81400689a7c5bbb315fc40597c72
author leeyn <leeyn.shun@gmail.com> 1728810556 +0300
committer leeyn <leeyn.shun@gmail.com> 1728810556 +0300

create Makefile
```

- Dumping Directory Tree:
    Use Git commands to dump the directory tree referenced by this commit.
```powershell
PS C:\Users\leeyn\work\hello\.git> git ls-tree f539aa9078557fafeaea1952e94bde778ccd3812
100644 blob 17883483456f52b454b98c64173b2a67a105e508    Makefile
040000 tree b409d9f629289f9fcccea88c3d42df689769ea55    lib
```

- Dump the contents of the lib/ directory and the hello.sh file using Git commands
```powershell
PS C:\Users\leeyn\work\hello\.git> git ls-tree -r f539aa9078557fafeaea1952e94bde778ccd3812
100644 blob 17883483456f52b454b98c64173b2a67a105e508    Makefile
100644 blob 524792eb8acd3d6ebdcf3cd24221fd0f03c44a2e    lib/hello.sh
PS C:\Users\leeyn\work\hello\.git> git show 524792eb8acd3d6ebdcf3cd24221fd0f03c44a2e
#!/bin/bash

# Default is World
# Author: Jim Weirich <jim.weirich@hello.world>
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
PS C:\Users\leeyn\work\hello> cat lib/greeter.sh
#!/bin/bash

Greeter() {
    who="$1"
    echo "Hello, $who"
}
PS C:\Users\leeyn\work\hello> git add lib/greeter.sh
warning: in the working copy of 'lib/greeter.sh', LF will be replaced by CRLF the next time Git touches it
PS C:\Users\leeyn\work\hello> git commit -m "adding greeter.sh"
[greet f9c830b] adding greeter.sh
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
PS C:\Users\leeyn\work\hello> git add lib/hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "modify hello.sh to use greeter"
[greet 637aa90] modify hello.sh to use greeter
 1 file changed, 7 insertions(+), 4 deletions(-)
```

- Update the Makefile with the following comment and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> cat Makefile
# Ensure it runs the updated lib/hello.sh file
TARGET="lib/hello.sh"

run:
        bash ${TARGET}
PS C:\Users\leeyn\work\hello> git add Makefile
PS C:\Users\leeyn\work\hello> git commit -m "add commets in Makefile"
[greet 4467c04] add commets in Makefile
 1 file changed, 1 insertion(+)
```

- Switch back to the main branch, compare and show the differences between the main 
    and greet branches for Makefile, hello.sh, and greeter.sh files.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Switched to branch 'master'
PS C:\Users\leeyn\work\hello> git diff greet -- Makefile
diff --git a/Makefile b/Makefile
index 1e4b9d8..1788348 100644
--- a/Makefile
+++ b/Makefile
@@ -1,4 +1,3 @@
-# Ensure it runs the updated lib/hello.sh file
 TARGET="lib/hello.sh"

 run:
PS C:\Users\leeyn\work\hello> git diff greet -- lib/hello.sh
diff --git a/lib/hello.sh b/lib/hello.sh
index 56a4589..524792e 100644
--- a/lib/hello.sh
+++ b/lib/hello.sh
@@ -1,10 +1,7 @@
 #!/bin/bash

-source lib/greeter.sh
+# Default is World
+# Author: Jim Weirich <jim.weirich@hello.world>
+name=${1:-"World"}

-name="$1"
-if [ -z "$name" ]; then
-    name="World"
-fi
-
-Greeter "$name"
\ No newline at end of file
PS C:\Users\leeyn\work\hello> git diff greet -- lib/greeter.sh
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
PS C:\Users\leeyn\work\hello> cat README.md
This is the Hello World example from the git project.
PS C:\Users\leeyn\work\hello> git add README.md
PS C:\Users\leeyn\work\hello> git commit -m "adding README.md"
[master bad1652] adding README.md
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

- Draw a commit tree diagram illustrating the diverging changes between all branches to demonstrate the branch history.
```powershell
PS C:\Users\leeyn\work\hello> git log --oneline --graph --all
* bad1652 (HEAD -> master) adding README.md
| * 4467c04 (greet) add commets in Makefile
| * 637aa90 modify hello.sh to use greeter
| * f9c830b adding greeter.sh
|/
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
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
PS C:\Users\leeyn\work\hello> 
```

- Switch to main branch and make the changes below to the hello.sh file, save and commit the changes.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Switched to branch 'master'

PS C:\Users\leeyn\work\hello> cat lib\hello.sh    
#!/bin/bash

echo "What's your name"
read my_name

echo "Hello, $my_name"
PS C:\Users\leeyn\work\hello> git add lib/hello.sh
PS C:\Users\leeyn\work\hello> git commit -m "read input for hello"
[master 0f23690] read input for hello
 1 file changed, 3 insertions(+), 4 deletions(-)
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
PS C:\Users\leeyn\work\hello> git merge --continue
[greet e282f04] Merge branch 'master' into greet
PS C:\Users\leeyn\work\hello> git log --oneline --all --graph
*   e282f04 (HEAD -> greet) Merge branch 'master' into greet
|\
| * 0f23690 (master) read input for hello
* | e9e1c11 Merge branch 'master' into greet
|\|
| * bad1652 adding README.md
* | 4467c04 add commets in Makefile
* | 637aa90 modify hello.sh to use greeter
* | f9c830b adding greeter.sh
|/
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
```

- Rebasing Greet Branch:
    Go back to the point before the initial merge between main and greet.
    Rebase the greet branch on top of the latest changes in the main branch.
```powershell
PS C:\Users\leeyn\work\hello> git reset --hard 4467c04
HEAD is now at 4467c04 add commets in Makefile
PS C:\Users\leeyn\work\hello> git log --oneline --all --graph
* 0f23690 (master) read input for hello
* bad1652 adding README.md
| * 4467c04 (HEAD -> greet) add commets in Makefile
| * 637aa90 modify hello.sh to use greeter
| * f9c830b adding greeter.sh
|/
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
PS C:\Users\leeyn\work\hello> git rebase master
Auto-merging lib/hello.sh
CONFLICT (content): Merge conflict in lib/hello.sh
error: could not apply 637aa90... modify hello.sh to use greeter
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config advice.mergeConflict false"
Could not apply 637aa90... modify hello.sh to use greeter
PS C:\Users\leeyn\work\hello> git add lib/hello.sh
PS C:\Users\leeyn\work\hello> git rebase --continue
[detached HEAD 4a21eb0] modify hello.sh to use greeter
 1 file changed, 1 insertion(+), 1 deletion(-)
Successfully rebased and updated refs/heads/greet.
PS C:\Users\leeyn\work\hello> git log --oneline --all --graph
* 29efb1c (HEAD -> greet) add commets in Makefile
* 4a21eb0 modify hello.sh to use greeter
* fff16fc adding greeter.sh
* 0f23690 (master) read input for hello
* bad1652 adding README.md
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
```

- Merging Greet into Main:
    Merge the changes from the greet branch into the main branch.
```powershell
PS C:\Users\leeyn\work\hello> git checkout master
Switched to branch 'master'
PS C:\Users\leeyn\work\hello> git merge greet
Updating 0f23690..29efb1c
Fast-forward
 Makefile       | 1 +
 lib/greeter.sh | 6 ++++++
 lib/hello.sh   | 2 +-
 3 files changed, 8 insertions(+), 1 deletion(-)
 create mode 100644 lib/greeter.sh
PS C:\Users\leeyn\work\hello> git log --oneline --all --graph
* 29efb1c (HEAD -> master, greet) add commets in Makefile
* 4a21eb0 modify hello.sh to use greeter
* fff16fc adding greeter.sh
* 0f23690 read input for hello
* bad1652 adding README.md
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
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
PS C:\Users\leeyn\work> cd cloned_hello
PS C:\Users\leeyn\work\cloned_hello> git log --oneline --all --graph
* 29efb1c (HEAD -> master, origin/master, origin/greet, origin/HEAD) add commets in Makefile
* 4a21eb0 modify hello.sh to use greeter
* fff16fc adding greeter.sh
* 0f23690 read input for hello
* bad1652 adding README.md
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
```

- Display the name of the remote repository and provide more information about it.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git remote
origin
PS C:\Users\leeyn\work\cloned_hello> git remote --v  
origin  C:/Users/leeyn/work/hello (fetch)
origin  C:/Users/leeyn/work/hello (push)
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
PS C:\Users\leeyn\work\hello> git commit -m "changed in original"
[master bc97f3b] changed in original
 1 file changed, 2 insertions(+), 1 deletion(-)
```

- Inside the cloned repository (cloned_hello), fetch the changes from the remote repository and display the logs. Ensure that commits from the hello repository are included in the logs.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git fetch origin
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 358 bytes | 22.00 KiB/s, done.
From C:/Users/leeyn/work/hello
   29efb1c..bc97f3b  master     -> origin/master
PS C:\Users\leeyn\work\cloned_hello> git log --oneline --all --graph 
* bc97f3b (origin/master, origin/HEAD) changed in original
* 29efb1c (HEAD -> master, origin/greet) add commets in Makefile
* 4a21eb0 modify hello.sh to use greeter
* fff16fc adding greeter.sh
* 0f23690 read input for hello
* bad1652 adding README.md
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
```

- Merge the changes from the remote main branch into the local main branch.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git merge origin/master
Updating 29efb1c..bc97f3b
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
* bc97f3b (origin/master, origin/HEAD, master) changed in original
* 29efb1c (HEAD -> greet, origin/greet) add commets in Makefile
* 4a21eb0 modify hello.sh to use greeter
* fff16fc adding greeter.sh
* 0f23690 read input for hello
* bad1652 adding README.md
* f539aa9 create Makefile
* 84d6ad2 moved hello.sh to lib
* 005f9d9 adding author info
* 1d089b5 (tag: v1) initialise name and echo
* bc714b2 (tag: v1-beta) comment on default value
* d04fdf6 second commit
* 2c4b412 first commit
```

- Add a remote to your Git repository and push the main and greet branches to the remote.
```powershell
PS C:\Users\leeyn\work\cloned_hello> git remote add gritLab https://01.gritlab.ax/git/ylee/git
PS C:\Users\leeyn\work\cloned_hello> git remote -v
gritLab https://01.gritlab.ax/git/ylee/git (fetch)
gritLab https://01.gritlab.ax/git/ylee/git (push)
origin  C:/Users/leeyn/work/hello (fetch)
origin  C:/Users/leeyn/work/hello (push)
PS C:\Users\leeyn\work\cloned_hello> git push gritLab
Enumerating objects: 38, done.
Counting objects: 100% (38/38), done.
Delta compression using up to 12 threads
Compressing objects: 100% (28/28), done.
Writing objects: 100% (38/38), 3.34 KiB | 570.00 KiB/s, done.
Total 38 (delta 4), reused 12 (delta 0), pack-reused 0 (from 0)
remote: . Processing 1 references
remote: Processed 1 references in total
To https://01.gritlab.ax/git/ylee/git
 * [new branch]      greet -> greet
PS C:\Users\leeyn\work\cloned_hello> git push gritLab master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 378 bytes | 378.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote:
remote: Create a new pull request for 'master':
remote:   https://01.gritlab.ax/git/ylee/git/compare/greet...master
remote:
remote: . Processing 1 references
remote: Processed 1 references in total
To https://01.gritlab.ax/git/ylee/git
 * [new branch]      master -> master
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
[master 97391a2] shared README
 1 file changed, 1 insertion(+), 1 deletion(-)
PS C:\Users\leeyn\work\hello> git push --set-upstream bareHello master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 398 bytes | 398.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To ../hello.git
   bc97f3b..97391a2  master -> master
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
Updating 29efb1c..97391a2
Fast-forward
 README.md | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
PS C:\Users\leeyn\work\cloned_hello> cat README.md
This is the Hello World example from the git project.
(Changed in the original and pushed to shared)
```
---
