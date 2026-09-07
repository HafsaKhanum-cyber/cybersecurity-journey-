# 🔎 Day 23 — File Investigation

## 🎯 Goal

Learn how to investigate files on Linux from a SOC Analyst perspective.

## 🛠️ Commands Learned

```bash
ls -la
ls -l
stat
file
find
cat
```

### What I learned

* `ls -la` → view files including hidden files
* `ls -l` → check permissions, owner, size and date
* `stat` → view detailed file metadata and timestamps
* `file` → identify the actual file type
* `find` → search for files
* `cat` → view file contents

## 🔍 Practical Investigation

I investigated:

* `confidential.txt`
* `confidential.txt.save`
* A file inside `/tmp/mintUpdate/`
* Hidden files such as `.bashrc`

I checked:

**Location → Owner → Permissions → Timestamps → File Type → Contents**

## 🧠 Key SOC Lesson

> **A hidden, random-looking, or suspiciously located file is not automatically malicious. Investigate it before making a conclusion.**

## ✅ Day 23 Completed
