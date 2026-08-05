day 9

detail on nmap 

part 1=theory
TYPES OF SCANS IN NMAP

1. TCP Connect Scan (-sT)

Command:

nmap -sT localhost

How it works:

Completes the full TCP Three-Way Handshake.

2. SYN Scan (-sS)

Command:

sudo nmap -sS localhost

How it works:

Sends only a SYN packet.
If it gets SYN-ACK, it knows the port is open.
It does not complete the full handshake.
Faster and commonly called a Stealth Scan.

3. Ping Scan (-sn)

Command:

nmap -sn 192.168.1.0/24

Purpose:

This scan discovers which hosts are alive without scanning their ports.


Part 2 – Practical Lab


1=Run:

nmap -sT localhost

Questions:

How many open ports do you see?

Answer:2

Are the results different from yesterday?

Answer:no,Both scans identified the same two open ports because the services running on your computer have not changed.


2=Run:

sudo nmap -sS localhost

Questions:

Does it find the same ports?

Answer:Yes, it finds the same open ports because the same host is being scanned.

Why does this command require sudo?

Answer:Because SYN scans use raw TCP packets, which require root privileges on Linux.


3=run: 
nmap -sn 192.168.1.0/24 
Questions: 
How many devices are online? 
Answer:3 are online 

Can you identify your own IP? 
Answer:Nmap scan report for h-Auron-Paine (192.168.1.107) 
yes i can


Part 3 – Think Like a SOC Analyst

Imagine you scan a company network.

You discover:

192.168.1.15
Host is up.

22/tcp open ssh
80/tcp open http
445/tcp open microsoft-ds
Questions
Which port would interest you first?
Why?
Port 80 (HTTP) interests me most because it handles website-related traffic. If the company's website is unavailable, this is the first service I would investigate to identify the cause of the problem.

Which service belongs to Windows?
Port 445 is used by SMB (Server Message Block), Microsoft's file and printer sharing protocol, so it is commonly associated with Windows systems.

