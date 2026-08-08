Day 13 – Linux Processes & Services

Objective

Learn how Linux manages running processes and background services, and understand how these can be monitored during security investigations.

Topics Learned

- Linux Processes
- Process ID (PID)
- CPU Usage
- Memory Usage
- Running Processes
- Linux Services
- Process Monitoring
- Basic SOC Investigation

Practical Work

- Used `ps` to view running processes
- Used `ps aux` to view detailed process information
- Used `top` to monitor processes in real time
- Identified process IDs (PIDs)
- Observed CPU and memory usage
- Used `systemctl` to view and investigate services
- Investigated a suspicious-process scenario from a SOC Analyst perspective

Key Takeaways

- A process is a program that is currently running.
- Every process has a unique Process ID (PID).
- `ps aux` provides detailed information about running processes.
- `top` allows processes to be monitored in real time.
- Linux services usually run in the background and provide specific functions.
- High CPU or memory usage does not automatically mean a process is malicious.
- SOC Analysts investigate unusual processes by examining their user, PID, resource usage, and behavior.

Status

✅ Completed
