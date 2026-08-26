Day 20 

— User & Privilege Investigation



1. `id` — Check User Information

Important:

* **UID** = User ID
* **GID** = Group ID
* **groups** = Groups the user belongs to


2. `groups` — Check Groups

Being in the `sudo` group means the account can have administrative privileges through `sudo`.


3. `getent passwd` — Check Account

Important information:

Username → h
UID → 1000
GID → 1000
Home → /home/h
Shell → /bin/bash

Shell

`/bin/bash` = interactive shell.

`/usr/sbin/nologin` = generally prevents interactive login.

Non-interactive does **not** automatically mean safe.


4. `who` — Current Sessions

`who` tells us:

> **Who is currently logged in?**

`:0` represents my local graphical session.


5. `w` — More Session Information

`w` shows current logged-in users plus more information about their sessions/activity.

Remember:

who → Who is logged in now?
w   → Who is logged in + more information


6. `last` — Login History

`last` shows previous login/session activity.

It can show:

* Username
* Login time
* Logout time
* Session duration
* Reboots
* Crashes

My output mainly showed:

h tty7 :0

So my history mainly contained local graphical sessions.

Remember:

who  → current sessions
last → previous sessions


7. `sudo -l` — Check Privileges

My important result:

(ALL : ALL) ALL

This means my account can use `sudo` to run commands with administrative privileges.

I also had some `NOPASSWD` Linux Mint commands.

`NOPASSWD`

Means a specific sudo command can be run without entering the sudo password.


8. `whoami` vs `sudo whoami`

Result:
h

Current user = `h`

Then:

sudo whoami

Result:
root

So:
h
 ↓ sudo
root

This demonstrates **privilege elevation**.


Privilege Escalation

Privilege escalation means:

> An attacker moves from lower privileges to higher privileges.

Example:

Attacker
 ↓
Compromises normal user
 ↓
Gets higher privileges
 ↓
Root

Root can perform highly privileged actions, so unexpected privilege escalation is important for SOC analysts.


SOC Investigation Workflow

Suspicious account
      ↓
Identify user
      ↓
Check UID/GID
      ↓
Check groups
      ↓
Check shell
      ↓
Check sudo privileges
      ↓
Check current sessions
      ↓
Check login history
      ↓
Check privileged activity
      ↓
Determine risk



— Mini Investigation Answers

1. What is your UID?

Answer:
UID = 1000

My username is `h`.


2. What groups does your account belong to?

Answer:
h
adm
cdrom
sudo
dip
plugdev
users
lpadmin
sambashare
wireshark

Important: I am a member of the `sudo` group'


3. Do you have `sudo` privileges?

Answer: Yes.

My `sudo -l` showed:

(ALL : ALL) ALL

This means my account can use `sudo` to perform administrative actions.

I also have some specific `NOPASSWD` commands.


4. What shell does your account use?

Answer:
/bin/bash

This is a normal **interactive shell**.


5. Is your current session visible in `who`/`w`?

Answer: Yes.

My `who` output showed:

h tty7 2026-08-23 20:41 (:0)
This means user `h` has a current local graphical session.


6. Does `last` show previous login activity?

Answer: Yes.

`last` showed many previous sessions for:
h tty7 :0

Most of them were local graphical sessions.

It also showed some `reboot` and `crash` records.


7. Why would a SOC analyst care if a normal user suddenly became a privileged user?

Answer:

Because it could indicate **privilege escalation**.

For example:

Attacker
 ↓
Compromises normal account
 ↓
Gains higher privileges
 ↓
Root

An attacker with root privileges can have much greater control over the system.
