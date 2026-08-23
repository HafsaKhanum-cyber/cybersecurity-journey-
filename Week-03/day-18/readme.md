# Day 18 — SIEM & Wazuh

## 🎯 What I Learned

* What a **SIEM** does in a SOC
* Basic **Wazuh architecture**
* Wazuh Agent, Server, Indexer and Dashboard
* Difference between an **event and an alert**
* How authentication events can become security alerts
* How SOC analysts investigate authentication failures

## 🧪 Practical Work

* Generated a controlled failed authentication attempt
* Investigated `/var/log/auth.log`
* Identified:

  * Timestamp
  * User
  * Target account
  * PID
  * Terminal
* Investigated the PID using `ps`
* Checked related authentication events
* Determined the event was **benign test activity**

## 🔑 Key Learning

> One failed authentication does not automatically mean an attack.
> Repeated failures, timing, source information and other evidence are needed to determine whether activity is suspicious.

## 🛠️ Tools/Commands

`SIEM` • `Wazuh` • `grep` • `ps` • `auth.log`

## ✅ Status

Day 18 completed.
