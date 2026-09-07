# 🔥 Day 22 — Network Connection Investigation

## 🎯 Goal

Learn how to investigate network connections and find:

**IP → Port → PID → Process → User → Executable → Destination**

## 1️⃣ Check Network Connections

Command:

ss -tunap


### Important states:

* `ESTAB` → Active connection
* `LISTEN` → Waiting for incoming connections
* `CLOSE-WAIT` → Remote side closed the connection

Example:

192.168.1.107:58092 → 172.64.148.235:443
Chrome PID 1919


**Important:** Port `443` does not automatically mean safe or malicious.

---

## 2️⃣ Find Chrome Connections

ss -tunap | grep chrome


This shows network connections belonging to Chrome.

Example:

172.64.148.235:443 → chrome, PID 1919


## 3️⃣ Investigate the Process


ps -p 1919 -o pid,user,comm,args


Result showed:

PID: 1919
User: h
Process: chrome

It was a:
Chrome Network Service


## 4️⃣ Check Process Network Activity

sudo lsof -p 1919 -i -n -P

This confirmed Chrome PID 1919 had multiple network connections.

Example:


192.168.1.107:58092 → 172.64.148.235:443


## 5️⃣ Check Executable


readlink -f /proc/1919/exe

Result:


/opt/google/chrome/chrome


This confirms the exact executable.


## 6️⃣ Check Command Line


tr '\0' ' ' < /proc/1919/cmdline


Important part:


--type=utility
--utility-sub-type=network.mojom.NetworkService

This confirmed PID 1919 is Chrome's **Network Service**.



## 7️⃣ Verify Process Owner


stat -c '%U %G' /proc/1919

Result:


h h

So the process belongs to user `h`.


## 8️⃣ Reverse DNS Lookup

host 172.64.148.235

Result:
NXDOMAIN

Meaning:

**No reverse DNS hostname was found.**

NXDOMAIN does NOT mean malicious.


## 9️⃣ Investigate IP Ownership


curl -s https://ipinfo.io/172.64.148.235

Result showed:

AS13335 Cloudflare, Inc.


The IP belongs to **Cloudflare infrastructure**.

We also checked:

104.18.32.47


It also belonged to:

AS13335 Cloudflare, Inc.


---

## 🔟 Identify Network Interface

ip -br link


My active Wi-Fi interface:

wlp1s0

## 1️⃣1️⃣ Capture Packets

sudo tcpdump -i wlp1s0 -c 20


Captured **20 packets** with:

0 packets dropped


Saw:

* DNS traffic
* UDP traffic
* HTTPS/QUIC traffic



## 1️⃣2️⃣ Capture DNS Traffic

sudo tcpdump -i wlp1s0 -c 10 port 53


Example:

A? chatgpt.com.
```

Response:

A 172.64.155.209
A 104.18.32.47


### DNS Records

* `A` → IPv4 address
* `AAAA` → IPv6 address
* `PTR` → Reverse DNS
* `NXDOMAIN` → No record found

---

# 🎯 SOC Investigation Chain

Network Connection
        ↓
IP + Port
        ↓
PID
        ↓
Process
        ↓
User
        ↓
Executable
        ↓
Command Line
        ↓
Destination Ownership
        ↓
SOC Conclusion


## 🧠 Final Lesson

A SOC analyst should **not assume a connection is malicious just because it uses an external IP or port 443**.

Instead:

> **Collect evidence → correlate it → investigate → then make a conclusion.**

### 🛠️ Commands Learned

ss
ps
grep
lsof
readlink
/proc
stat
host
curl
ip -br link
tcpdump

