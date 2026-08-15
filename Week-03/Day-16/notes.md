Day 16 
— SSH & Brute-Force Investigation

Part 1 — SSH

SSH = Secure Shell

It is used to securely connect to and control a Linux computer remotely.

SSH normally uses port 22.

— Check SSH service

systemctl status ssh

→ Checks whether the SSH service is running.

My result:
Unit ssh.service could not be found

→SSH server/service is not installed or registered on my system.

— Search SSH activity in logs


sudo grep -i "ssh" /var/log/auth.log


— Failed SSH attempts

sudo grep "Failed password" /var/log/auth.log


→ Finds failed SSH password attempts in the authentication log.

— Reading a failed SSH log

Failed password for invalid user admin from 192.168.1.50 port 45678 ssh2


**Failed password** → authentication failed

**invalid user admin** → attempted username does not exist

**192.168.1.50** → source IP

**port 45678** → source port

**ssh2** → SSH protocol


— Brute Force

**Brute-force attack** → repeatedly trying passwords or credentials to gain access.

Example:

```text
Failed
Failed
Failed
Failed
Failed
```

Many failed attempts from the same source can be suspicious and should be investigated.

— Extract information with awk


awk

→ Used to extract specific information/fields from text.


sudo grep "Failed password" /var/log/auth.log | awk '{print $NF}'

→ Searches failed password attempts and extracts a specific field from the results.

— Count repeated activity


sudo grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c


→ Finds failed attempts, extracts information, sorts it and counts repeated values.

Commands used:


grep → finds the relevant log entries
awk → extracts information
sort → sorts the results
uniq -c → counts repeated results



Part 2— SOC Investigation

If one IP has:

```text
192.168.1.50 → 37 failed attempts
10.0.0.20    → 2 failed attempts
172.16.0.5   → 1 failed attempt
```

I would investigate **192.168.1.50 first** because it has the highest number of failed attempts.

But I would **not immediately call it an attacker**.

I would investigate:

* Source IP
* Username
* Time
* Number of attempts
* Whether login eventually succeeded
* What happened after the login


"keytakeaway"
My system did not have SSH service/SSH authentication records, so SSH failed-login searches returned no relevant results. I learned that investigation commands depend on the logs/events actually present on the system.
