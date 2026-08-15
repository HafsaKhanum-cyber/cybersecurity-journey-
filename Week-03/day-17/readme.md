# Day 17 — Network Connection & Process Investigation

## Objective

Investigate an unknown external network connection and learn how to connect network evidence with the process and user responsible for it.

## Topics Learned

- Active network connections
- External IP addresses
- Ports
- Network processes
- PID (Process ID)
- Users associated with processes
- False positives
- Multi-tool SOC investigation
- Evidence-based investigation

## Tools Used

- `ss`
- `lsof`
- `ps`

## Practical Investigation

### Step 1 — Identify Network Connections

```bash
ss -t
