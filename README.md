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
```
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
```
PS C:\Users\leeyn\work\hello> cat hello.sh
echo "Hello, World"
```

- Initialize the git repository in the hello directory.
```
PS C:\Users\leeyn\work\hello> git init
Initialized empty Git repository in C:/Users/leeyn/work/hello/.git/
```

- Check the status and act accordingly with the output of the executed command.
```
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
```
PS C:\Users\leeyn\work\hello> cat hello.sh
#!/bin/bash

echo "Hello, $1"
```

- Stage the changed file and commit the changes, the working tree should be clean.
```
PS C:\Users\leeyn\work\hello> git add hello.sh
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
PS C:\Users\leeyn\work\hello> git commit -m "second commit"
[master e1cc968] second commit
 1 file changed, 3 insertions(+), 1 deletion(-)
```

- Modify the hello.sh file to include comments and stage it.
```
PS C:\Users\leeyn\work\hello> cat .\hello.sh 
#!/bin/bash

# Default is "World"
name=${1:-"World"}
echo "Hello, $name"
''''

- Make two separate commits:
- The first commit should be for the comment in line 3.
''''
PS C:\Users\leeyn\work\hello> git add -p hello.sh
warning: in the working copy of 'hello.sh', LF will be replaced by CRLF the next time Git touches it
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
```
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
