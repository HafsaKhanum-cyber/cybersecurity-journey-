Day 15 – Linux Logs & Security Investigation

Objective

Learn how Linux logs record system activity and how SOC Analysts can use logs to investigate suspicious activity and authentication events.

Topics Learned

- Linux System Logs
- `/var/log`
- Authentication Logs
- `tail`
- `tail -f`
- `grep`
- `journalctl`
- Failed Authentication Attempts
- Log Investigation
- SOC Investigation

Practical Work

- Explored the `/var/log` directory
- Inspected Linux log files
- Used `tail` to view recent log entries
- Used `tail -f` to monitor new log entries
- Used `grep` to search logs for specific patterns
- Investigated failed authentication attempts
- Used `journalctl` to view system logs
- Used error-level filtering with `journalctl`
- Practiced investigating Linux activity from a SOC Analyst perspective

Key Takeaways

- Logs provide a record of events occurring on a system.
- SOC Analysts use logs as evidence during investigations.
- `tail` can be used to view recent log entries.
- `tail -f` can continuously monitor new log entries.
- `grep` can search logs for specific words or patterns.
- `journalctl` can be used to view and investigate system logs.
- Multiple failed authentication attempts can be a reason for further investigation, but they do not automatically mean a system has been compromised.
- Analysts should investigate the user, time, source IP, and activity surrounding a suspicious event before reaching a conclusion.

Commands Learned

`tail` → Shows the last lines of a file or log.

`tail -f` → Continuously shows new log entries as they appear.

`grep` → Searches text or logs for a specific word or pattern.

`journalctl` → Views and searches system logs.

Status

✅ Completed
