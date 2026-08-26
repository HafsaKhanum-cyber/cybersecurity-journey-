Day 21 

— Endpoint & Process Investigation


Commands Used

ps aux --sort=-%cpu | head -10
View running processes.


ps -p 4011 -f
Investigate a specific process.


ps -p 1916 -f
Investigate the parent process.


readlink -f /proc/4011/exe
Find the executable path.


tr '\0' ' ' < /proc/4011/cmdline
View command-line arguments.


sudo lsof -Pan -p 4011 -i
Check network connections of the process.


s -p 4011 -o user,pid,ppid,cmd
View user, PID, PPID and command together.


PID vs PPID


PID  = Who am I?
PPID = Who is my parent?


Our process:

Chrome Zygote
PID 1916
    ↓
Chrome Renderer
PID 4011

**Chrome Renderer** → handles webpage content.

**Chrome Zygote** → prepared Chrome process that helps create certain Chrome child processes.



Investigation Result

| Item       | Result                                        |
| ---------- | --------------------------------------------- |
| Process    | Chrome Renderer                               |
| PID        | `4011`                                        |
| PPID       | `1916`                                        |
| User       | `h`                                           |
| Executable | `/opt/google/chrome/chrome`                   |
| Arguments  | `--type=renderer` + Chrome internal arguments |
| Network    | No connection shown                           |
| Result     | No obvious suspicious activity                |



Questions & Answers

**1. What process did you investigate?**
→ Chrome Renderer.

**2. What was its PID?**
→ `4011`

**3. What was its PPID?**
→ `1916`

**4. Which user owns it?**
→ `h`

**5. What executable is running?**
→ `/opt/google/chrome/chrome`

**6. What command-line arguments did you find?**
→ `--type=renderer` and other Chrome internal arguments.

**7. Does it have network connections?**
→ No connection was shown by `lsof`.

**8. Does anything look suspicious?**
→ No obvious suspicious activity based on the evidence collected.



SOC Lesson

> **Don't judge a process from one clue. Check the user, parent, executable, command line, network activity and overall context before deciding whether it is suspicious.**


PID → User → PPID → Parent → Executable → Command Line → Network → Decision

