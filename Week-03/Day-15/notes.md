day 15

— SOC ANALYST & LOG INVESTIGATION
— Linux Logs & Security Investigation


A SOC analyst doesn't only look at network traffic. They also look at system events and logs to understand what happened.

part 1

-log=event that took place in computer

— Explore /var/log

Run:

ls /var/log

Question

Look at your output.

What log files/directories can you see?

Write:

1.auth.log— Records login, authentication, and `sudo` activity.
2.syslog— Records general system events, services, and errors.
3.ufw.log— Records firewall activity, including blocked or allowed connections.
4.apache2— Contains web-server logs showing website requests and errors.


— Read a Log

inspect a log safely.

run:

sudo tail /var/log/auth.log

— tail -f

This one is especially useful for monitoring.

Run:

sudo tail -f /var/log/auth.log

It keeps watching the file for new entries.


— grep

grep searches text for something specific.

For example:

grep "failed" /var/log/auth.log

This attempts to find lines containing:

failed

—Run:

sudo journalctl

This displays logs collected by systemd's journal.

Because there can be a huge amount of output,so run:

sudo journalctl -n 20

This shows the latest 20 entries.

Then:

sudo journalctl -p err -n 20

This focuses on recent error-level messages.


part 2— Your SOC Scenario

Imagine you receive this alert:

> 🚨 **Alert:** Multiple failed authentication attempts detected on a Linux server.

You have access to:

grep
journalctl
tail

*Question

*Which command would you use first to search specifically for failed authentication attempts?**

Your answer,Why?

i will use grep to specifically find the failed attempts.Because grep searches the log for a specific word or pattern, so it can quickly find authentication attempts containing “failed”.
