week 2
day 8


part 1=theory
– What is Nmap?
It answers questions like:

Is the computer online?
Which ports are open?
Which services are running?
Which operating system might it be using?

Nmap does not hack a system. It gathers information. This process is called reconnaissance (recon).

Host

A host is any device connected to a network.

Port

A port is a logical communication endpoint used by applications.

Service

A service is a program listening on a port.


Understanding Port States

Nmap mainly reports three states.

Open

The port is accepting connections.

Closed

The port exists but nothing is listening.

Filtered

Nmap cannot determine whether the port is open because something (often a firewall) is blocking the probe.



part 2= practical

Command 1

nmap localhost

Questions
How many open ports do you see?

Answer:2

Which services are running?

Answer:http,ipp 


Command 2 

nmap 127.0.0.1

Question: Are the results different from localhost? 
Why or why not?

Answer:only time diffrence occured apart from time the results are same because i am using ip address of localhost so i write domain name or ip address the result will  be same


Command 3

1=hostname -I
2=nmap 192.168.1.107

Question:

Do you get the same results as scanning localhost?

Answer: No, the results are different. Scanning localhost showed ports 80 and 631 open, while scanning 192.168.1.107 showed only port 80. This is because localhost uses the loopback interface inside the computer, while 192.168.1.107 uses the local network interface. The IPP service (port 631) is configured to listen only on the localhost interface, so it is not accessible through the local network IP.


Command 4

nmap -sV localhost

The -sV option asks Nmap to identify the versions of detected services.

Questions

What additional information do you see compared to the previous scan?

Answer:The -sV scan shows the software and version running on the open ports.

Part 3 – Think Like a SOC Analyst

Imagine you scan a company server and get:

22/tcp    open    ssh
80/tcp    open    http
443/tcp   open    https
Question

Which service would you investigate first if the company says:

"Our website is unavailable."

Write your reasoning.

Answer:I would first investigate HTTP (port 80) and HTTPS (port 443) because they are responsible for serving the company's website.


