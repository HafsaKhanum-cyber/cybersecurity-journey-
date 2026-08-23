# Day 18 — SIEM & Wazuh: Authentication Investigation

## 🎯 Goal

Learn how a SIEM such as Wazuh helps a SOC analyst collect security events, generate alerts, and investigate suspicious activity.

Today I focused on **authentication events and practical log investigation**.

---

## 🧠 What I Learned

### SIEM

A SIEM collects and organizes security events so SOC analysts can search, monitor, detect, and investigate suspicious activity.

### Wazuh Components

I learned the basic role of:

* **Wazuh Agent** → Collects security information from an endpoint
* **Wazuh Server** → Processes and analyzes events
* **Wazuh Indexer** → Stores and indexes security data
* **Wazuh Dashboard** → Allows analysts to view and investigate events

### Event vs Alert

**Event:** Something happened on a system.

Example:

```text
Failed authentication
```

**Alert:** A detection system identifies an event or pattern that requires attention.

Example:

```text
Multiple authentication failures
```

---

# 🔎 Practical Investigation

I generated a controlled failed authentication attempt on my own Linux machine using:

```bash
su -
```

I intentionally entered an incorrect password.

Then I investigated the resulting authentication event.

### Command Used

```bash
sudo grep -i "failed" /var/log/auth.log | tail -10
```

This allowed me to search authentication logs for failed events.

I found:

```text
FAILED SU (to root) h on pts/1
```

---

## 🔍 Event Analysis

Important information from the event:

| Field       | Finding      |
| ----------- | ------------ |
| Time        | 17:46:08     |
| User        | h            |
| Target      | root         |
| Process     | su           |
| PID         | 4300         |
| Terminal    | pts/1        |
| Remote host | Not recorded |

I then investigated the PID:

```bash
ps -p 4300 -f
```

The process was no longer running because the `su` process had already ended.

This taught me that **logs can preserve evidence of processes that no longer exist**.

---

# 🧪 Session Investigation

I searched for events associated with the terminal:

```bash
sudo grep "pts/1" /var/log/auth.log
```

This showed:

```text
authentication failure
FAILED SU (to root)
```

The events occurred approximately one second apart.

Because I intentionally generated the failed authentication, I could determine that this was **benign test activity**, not an attack.

---

# 🚨 SOC Investigation Thinking

I learned that one failed authentication does not automatically mean an attack.

For example:

```text
1 failed attempt
→ Could be normal
```

But:

```text
Many failed attempts
+
Short time period
+
Same account
+
Same source
```

could indicate a possible **brute-force/password-guessing pattern**.

I also learned:

> Suspicious activity is not automatically confirmed malicious activity. An analyst needs evidence and context.

---

# 🔗 SOC Investigation Workflow

```text
SIEM Alert
    ↓
Examine the event
    ↓
Identify timestamp
    ↓
Identify user/account
    ↓
Identify source/session
    ↓
Look for repeated activity
    ↓
Investigate related evidence
    ↓
Determine whether activity is
benign or suspicious
    ↓
Make a conclusion
```

---

# 🛠️ Commands Used

```bash
sudo grep -i "authentication\|failed\|accepted" /var/log/auth.log | tail -30
```

```bash
sudo grep -i "failed password" /var/log/auth.log
```

```bash
sudo grep -i "failed" /var/log/auth.log | tail -10
```

```bash
ps -p 4300 -f
```

```bash
sudo grep "pts/1" /var/log/auth.log
```

---

# 💡 Key Lessons

* A SIEM centralizes and organizes security events.
* An event is not necessarily an alert.
* Repeated authentication failures can indicate suspicious activity.
* Context is important before declaring an incident malicious.
* Logs provide historical evidence.
* A process may no longer exist when an analyst investigates its historical log entry.
* `grep` helps locate evidence, but the analyst must interpret the evidence.
* Source IP, username, timestamps, frequency, and authentication results are important investigation data.

