# Day 16 — SSH & Brute-Force Investigation

## Objective

Learn how to investigate SSH authentication activity and understand how repeated failed login attempts can indicate a possible brute-force attack.

## Topics Learned

- SSH (Secure Shell)
- SSH authentication
- SSH port 22
- Authentication logs
- Failed authentication attempts
- Brute-force attacks
- Source IP investigation
- Log analysis
- `awk`
- `sort`
- `uniq`

## Practical Work

- Checked whether the SSH service was available using `systemctl status ssh`
- Found that SSH service was not installed/registered on my system
- Searched `/var/log/auth.log` for SSH-related activity
- Searched authentication logs for failed password attempts
- Learned how to read SSH authentication log entries
- Learned how source IPs can help identify the origin of login attempts
- Learned how repeated authentication failures can form a suspicious pattern
- Practiced using `awk` to extract information from log entries
- Learned how `sort` and `uniq -c` can help identify repeated activity

## Important Investigation Concept

A suspicious IP should not immediately be considered an attacker.

An analyst should investigate:

- Source IP
- Username
- Timestamp
- Number of attempts
- Whether authentication eventually succeeded
- What happened after a successful login

## Important Lesson

My system did not have SSH authentication records to investigate.

This taught me that investigation commands depend on the events and logs actually present on the system.

A command returning no results does not necessarily mean the command is wrong. It can mean that the searched event does not exist in the available logs.

## Commands Learned

`systemctl status ssh` → Checks the status of the SSH service.

`grep -i "ssh"` → Searches logs for SSH-related activity.

`grep "Failed password"` → Searches authentication logs for failed password attempts.

`awk` → Extracts specific fields from text or log output.

`sort` → Sorts command output.

`uniq -c` → Counts repeated lines/values.

## SOC Investigation Flow

Authentication Event  
↓  
Source IP  
↓  
Username  
↓  
Number of Attempts  
↓  
Successful or Failed Login  
↓  
Activity After Login  
↓  
Determine Whether Further Investigation Is Required

## Status

✅ Day 16 Completed
