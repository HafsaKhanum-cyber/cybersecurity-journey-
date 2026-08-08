day 12

Part 1 

— Users
Run:

whoami

This tells you the username of the account you're currently using.

— Groups
Run:

groups

This shows the groups your user belongs to.

Groups allow Linux administrators to give the same permissions to multiple users.

— File Ownership

Create a test directory:
run
mkdir day12

run
cd day12

Create a test file:
run
touch test.txt

Now run:
ls -l

the output:
-rw-rw-r-- 1 h h 0 Aug  8 18:47 test.txt

— Understanding Permissions

-rw-rw-r--

into:

-rw- rw- r--
 │    │   │
 │    │   └── Others
 │    └────── Group
 └─────────── Owner

There are three permission categories:

Owner

The user who owns the file.

Group

Users belonging to the file's group.

Others

Everyone else.

— Read, Write, Execute

There are three basic permissions:

r = Read

Can view the contents.

w = Write

Can modify the contents.

x = Execute

Can execute a file or enter a directory.

Remember:

r = read
w = write
x = execute

— chmod

chmod changes file permissions.

First check:

ls -l test.txt

Then run:

chmod 600 test.txt

Check again:

ls -l test.txt

the output:
-rw------- 1 h h 0 Aug  8 18:47 test.txt

This means:

Owner → read + write
Group → no permission
Others → no permission

Think Like a Security Analyst

Why might restricting a sensitive file to the owner be useful?

Answer:o unauthorized person will be able to access file except the owner

— Permission Numbers

Linux also represents permissions with numbers.

Read    = 4
Write   = 2
Execute = 1

Therefore:

chmod 600 test.txt

means:

Owner  = 6 → rw-
Group  = 0 → ---
Others = 0 → ---

— chown

chown changes the owner of a file.

Basic format:

chown USER FILE

Part 2 — SOC Investigation

Imagine you are investigating a Linux server.

You discover:

passwords.txt

and its permissions are:

-rw-rw-rw-
Question

Would this concern you?

Why?

Answer:The passwords are one of the things that need to be secure and protected from unauthorized access. rw for the owner, group, and others means everyone can read and modify the file. This is a big security concern for any organization.

