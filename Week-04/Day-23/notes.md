🔎 Day 23 — File Investigation

## 🎯 Goal

Learn how a SOC/Cyber Security Analyst investigates files on a Linux system.

The main idea is:

> **Don't judge a file by its name. Investigate it.**

We check:

* Where the file is
* Who owns it
* Its permissions
* Its timestamps
* Its actual file type
* Its contents
* Whether its behavior looks normal or suspicious

---

# 🧠 1. `ls -la`

ls -la
```

### What does it do?

Lists files in a directory with detailed information.

* `ls` → list files
* `-l` → long/detailed format
* `-a` → show hidden files too

Example hidden files:

.bashrc
.bash_history
.profile
```

### Important

A file beginning with `.` is normally hidden in Linux.

> **Hidden does NOT mean malicious.**

---

# 🔐 2. `ls -l`

ls -l ~/confidential.txt
```

Used to check basic file information.

Example:

-rw------- 1 h h 29 Mar 9 21:14 /home/h/confidential.txt
```

### Understanding permissions

-rw-------
```

* `-` → regular file
* `rw-` → owner can read and write
* `---` → group has no permission
* `---` → others have no permission

So this file has:

0600
```

Meaning:

> Only the owner can read and write the file.

### Other information

h h
```

→ owner and group

29
```

→ file size in bytes

Mar 9 21:14
```

→ last modification time

---

# 📋 3. `stat`

stat ~/confidential.txt
```

`stat` gives much more detailed information about a file.

It showed:

Size: 29
Inode: 7259263
Uid: 1000/h
Gid: 1000/h
Access
Modify
Change
Birth
```

### Important timestamps

**Access** → when the file was accessed/read.

**Modify** → when the file contents were changed.

**Change** → when file metadata/attributes changed.

**Birth** → when the file was created, when the filesystem provides this information.

### 🧠 SOC importance

Timestamps can help create a timeline.

For example:

> Was the file created before or after a suspicious event?

---

# 📄 4. `file`

```bash
file ~/confidential.txt
```

Output:

ASCII text
```

### What does `file` do?

It identifies the **actual type of a file** by examining its contents.

This is useful because a filename or extension can be misleading.

For example:

photo.jpg
```

doesn't automatically mean the file is really an image.

So:

> `file` helps us determine what the file actually is.

---

# 🔎 5. `find`

find ~ -name "confidential.txt"
```

### What does it do?

Searches for a file.

* `find` → search
* `~` → your home directory
* `-name` → search by filename
* `"confidential.txt"` → filename we're looking for

It found:

/home/h/confidential.txt
```

### Simple meaning

> "Find this file somewhere inside my home directory."

---

# 👀 6. `cat`

cat ~/confidential.txt
```

### What does it do?

Displays the contents of a text file in the terminal.

We found:

Salary Record: Manager = 000
```

We also investigated:

confidential.txt.save
```

and found:

Salary Record: Manager = $5000
Do not share this file.
```

The `.save` file appeared to be an older saved/backup version because it had an earlier timestamp, but we cannot prove exactly why it existed just from these commands.

### Important

`cat` normally **only displays** the contents. It doesn't modify the file.

---

# 🗂️ 7. Investigating `/tmp`

We searched `/tmp`:

find /tmp -type f
```

### What is `/tmp`?

`/tmp` is a Linux directory used for temporary files.

It can contain files created by:

* Applications
* System services
* Installers
* Update managers
* Other temporary processes

Because temporary directories can also be abused by attackers, SOC analysts may investigate unusual files there.

### We found:

/tmp/mintUpdate/enuvx38v
```

The filename looked random, so we investigated it.

First:

file /tmp/mintUpdate/enuvx38v
```

Result:

ASCII text
```

Then:

cat /tmp/mintUpdate/enuvx38v
```

The contents showed:

Launching Update Manager
Checking for updates
Found 171 software updates
Refreshing cache
Refreshing cache for Flatpak updates
```

### Conclusion

The file was a **Linux Mint Update Manager log**.

It was not suspicious based on what we observed.

### 🧠 Lesson

A random filename does not automatically mean malware.

We investigated it instead of assuming.

---

# 👻 8. Hidden File Investigation

We searched for hidden files:

find ~ -maxdepth 1 -type f -name ".*"
```

### Breaking it down

find
```

→ search

~
```

→ home directory

-maxdepth 1
```

→ don't go inside subdirectories

-type f
```

→ only regular files

-name ".*"
```

→ filenames beginning with `.`

We found files such as:

.bashrc
.bash_history
.profile
.Xauthority
.xsession-errors
```

These are normal Linux/user configuration files.

---

# 🖥️ 9. Investigating `.bashrc`

We checked:

ls -l ~/.bashrc
```

Then:

cat ~/.bashrc
```

`.bashrc` is a Bash configuration file.

It contains things such as:

aliases
history settings
terminal prompt settings
bash completion
```

For example:

alias ll='ls -alF'
```

creates the shortcut:

ll
```

### 🚨 Why did we investigate `.bashrc`?

Because shell configuration files can sometimes be abused for **persistence**.

Persistence means:

> An attacker tries to make something continue running or return automatically after a restart, login, or other event.

Our `.bashrc` contained normal configuration commands and showed **no obvious malicious persistence**.

---

# 🔥 SOC File Investigation Workflow

When a SOC analyst receives an alert about a suspicious file:

             Suspicious File
                    ↓
             Where is it?
                    ↓
              Who owns it?
                    ↓
             What permissions?
                    ↓
              When created?
                    ↓
           When modified/accessed?
                    ↓
             What type is it?
                    ↓
            What is inside it?
                    ↓
          Is the activity expected?
                    ↓
              CONCLUSION
```

---

# 🛠️ Commands Learned

| Command  | Purpose                                |
| -------- | -------------------------------------- |
| `ls -la` | List files including hidden files      |
| `ls -l`  | View permissions, owner, size and date |
| `stat`   | View detailed file metadata            |
| `file`   | Identify actual file type              |
| `find`   | Search for files                       |
| `cat`    | View file contents                     |

---

# 🧠 Most Important Lessons

### 1. Hidden doesn't mean malicious

.bashrc
```

is hidden, but completely normal.

### 2. Random filename doesn't mean malware

/tmp/mintUpdate/enuvx38v
```

looked unusual, but investigation showed it was an Update Manager log.

### 3. Don't trust the filename alone

Always investigate the actual file type and contents.

### 4. Timestamps are important

They can help us build a timeline of activity.

### 5. File permissions matter

They tell us who can read, write, or execute a file.

### 6. Context matters

A file in `/tmp` deserves investigation, but its location alone doesn't prove malicious activity.

---

# 🎯 Day 23 Conclusion

Today I learned how to investigate Linux files like a beginner SOC analyst.

I practiced checking:

**Location → Ownership → Permissions → Metadata → Timestamps → File Type → Contents → Context**

The biggest lesson:

> **Don't assume. Investigate first, then make a conclusion.**
