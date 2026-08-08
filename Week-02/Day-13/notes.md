day 13

Part 1 — What Is a Process?

A process is a program that is currently running.

For example, when you open:

Firefox
Terminal
Wireshark

Linux creates processes for them.

— View Processes

Run:

ps

This shows processes associated with your current terminal.

Important columns

PID

The process ID.

TTY

The terminal associated with the process.

CMD

The command/program running.

— View More Processes

Run:

ps aux

This gives you much more information.

Look for:

USER
PID
%CPU
%MEM
COMMAND

Question

Which process is using the most CPU?
Which process is using the most memory?

answer=The Google process (PID 2190) is using 18.4% CPU. and memory too 10.9

— Live Process Monitoring

Run:

top

will see processes updating in real time.

This is useful when investigating:

"Why is this computer suddenly very slow?"

Look at:

CPU usage
Memory usage
Running processes

To exit top, press:

q

— Linux Services

A service is a program designed to run in the background and provide a function.

Examples:

SSH
Web Server
Database
DNS

On modern Linux systems, systemd commonly manages services.

Run:

systemctl --type=service --state=running

This shows currently running services.

— Check a Specific Service

run:

systemctl status ssh

active or inactive 
in result


— Why SOC Analysts Care

because if high cpu usage and unknown process than it could be possibility of suspicious activity

Part 2— SOC Investigation

Imagine you receive this alert:

"A Linux server suddenly became extremely slow."

You check `top` and discover:

PID: 4312
CPU: 98%
USER: www-data
COMMAND: unknown-process

Question

What would you investigate first?

Answer:process id and will find out more information with ps aux and will investigate the process running on my computer

