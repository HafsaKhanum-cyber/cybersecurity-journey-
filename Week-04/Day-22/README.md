# Day 22 — Network Connection Investigation

## 🎯 Goal

Learn how to investigate network connections and identify which processes are communicating over the network.

## 🔹 What I Learned

* Network connections can reveal suspicious activity.
* `ss` shows active network connections and listening ports.
* A connection can be linked to a specific process/PID.
* `curl` can be used to investigate an IP address.
* Public IP information can help identify the location/organization associated with an IP.
* SOC analysts investigate **IP → connection → process → user**.

## 🔧 Commands Used

```bash
ss -tunap
```

Shows TCP/UDP connections and the processes using them.

```bash
curl -s https://ipinfo.io/<IP>
```

Gets basic information about a public IP.

## 🧠 Key SOC Idea

> Don't just look at an IP address.
> Ask: **Who connected to it? Which process made the connection? Which user owns that process?**

## ✅ Day 22 Completed

* Network connections investigated
* Processes linked to connections
* Public IP investigated
* SOC investigation workflow practiced
