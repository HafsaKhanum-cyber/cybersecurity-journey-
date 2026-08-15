day 17

Part 1 — Discover Active Connections

Run:

ss -t

Question 1: Which external IP appears most?**
My answer: none cz all are different

Question 2: Which port is being used?**
My answer:443 mostly and 1 is different

Question 3: Is it HTTPS (443) or something else?**
My answer: yes it is https mostly 1 is different


— Who Owns This Connection? 

Now install nothing—just investigate.

Run:

sudo lsof -i

What is `lsof`?

lsof = List Open Files

In Linux:

Network connections are files.

So `lsof` tells us which program owns the connection.

task

Find and fill:

- Command=chrome
- PID=2240
- User=h

— Investigate the Process

Run:

ps -p 2240 -f


Question

Process name=2240
User=h
Expected application=chrome


--the evidence chain

External IP=172.64.148.235      
      ↓
Port=443(https_
      ↓
PID=2240
      ↓
Process=chrome
      ↓
User=h


— New SOC Concept: False Positives

the alert says:

🚨 Unknown external IP detected.

You investigate and discover:

Process: chrome
Destination: Google HTTPS

Is this an attack?

No.

This is called a false positive.

Definition

A false positive is an alert that looks suspicious but turns out to be legitimate activity.


Part 2 — Practical Scenario


Alert:
Unknown external IP communicating over port 443


Evidence:
Process = chrome
User = h
Destination = HTTPS
Question 1

Would you immediately escalate this incident?
no

Why?
i will 1st investigate

Question 2

What additional evidence would you collect before making a conclusion?

Think about:

Logs

Process

User activity

Destination reputation

Your answer:i will 1st check logs because it can give me direct evidence and i can get to a conclusion if too investigate furhter more or not


Part 3— Mini Challenge (No Hints)

A SOC analyst receives:

External IP: 203.0.113.45
Port: 4444
Process: unknown-app
User: www-data

Without using Google—

What is the first thing you would investigate next?

Write your reasoning:

sudo lsof -i because I can know what connection is running right now with this specific IP and will get to know the process then


<>to know pid i should 1st use lsfo so i was right and we know unknown app means the process is still not known z its unknown and to know about it i will use lsfo to get its pid thats means 1st lsfo then process investigation.
