Day 14 – Linux Networking & System Investigation

Objective

Learn how to investigate Linux networking information, active connections, listening ports, and web communication using Linux commands.

Topics Learned

- Linux Network Interfaces
- IP Addresses
- Routing Table
- Default Gateway
- Network Sockets
- Listening Ports
- TCP and UDP Connections
- ping
- curl
- ss
- Basic Network Investigation
- SOC Analyst Investigation

Practical Work

- Used `ip a` to view network interfaces and IP addresses
- Used `ip route` to identify the default gateway and routing information
- Used `ss` to view network sockets
- Used `ss -tuln` to identify listening TCP and UDP ports
- Used `ping` to test network connectivity
- Used `curl` to communicate with a web server
- Used `curl -I` to inspect HTTP response headers
- Investigated a hypothetical suspicious network connection

Key Takeaways

- `ip a` shows network interfaces and IP addresses.
- `ip route` shows the routing table and default gateway.
- `ss` can be used to investigate network connections and sockets.
- Listening ports can help identify services running on a system.
- `ping` can be used to test network connectivity.
- `curl` can communicate with web servers and inspect HTTP responses.
- SOC Analysts can combine process and network information when investigating suspicious activity.

Command Revision

- `mkdir` – creates a directory
- `pwd` – shows the current working directory
- `ip a` – shows network interfaces and IP addresses
- `ps aux` – shows detailed information about running processes
- `chmod` – changes file and directory permissions

Status

✅ Completed
