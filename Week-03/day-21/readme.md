# Day 21 — Endpoint & Process Investigation

## 🎯 What I Learned

* Processes and process IDs (PID)
* Parent process ID (PPID)
* Parent-child process relationships
* Process owners
* Executable paths
* Command-line arguments
* `/proc` process information
* Process network activity
* How SOC analysts investigate suspicious processes

## 🧪 Practical Work

* Selected and investigated a Chrome renderer process
* Identified its PID, PPID and owner
* Investigated its parent process (Chrome zygote)
* Found the executable path
* Checked command-line arguments
* Checked network connections
* Made an evidence-based assessment of the process

## 🛠️ Commands

`ps` • `readlink` • `/proc` • `tr` • `lsof`

## 🔑 Key Learning

> A process should not be considered suspicious from one clue. Analysts investigate its owner, parent process, executable, command line and network activity together.

## ✅ Status

Day 21 completed.
