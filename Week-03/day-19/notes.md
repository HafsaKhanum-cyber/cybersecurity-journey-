Day 19 

— Authentication Attacks & Brute-Force Investigation


1. Authentication Failure

An **authentication failure** means:

> Someone tried to authenticate/login but the authentication failed.

We investigated:

authentication failure

Our actual event:

2026-08-16 17:46:07
authentication failure
ruser=h
user=root
rhost=


2. `FAILED SU`

sudo grep -ai "FAILED SU" /var/log/auth.log

Important event:

FAILED SU (to root) h on pts/1

Meaning:

> User `h` tried to switch to `root`, but authentication failed.

answers

**Who attempted it?**

> `h` 

**Which account was targeted?**

> `root`

**Remote or local?**

> Local


3. Important Log Lesson

found two events:

17:46:07.117190 → authentication failure
17:46:08.577156 → FAILED SU

The second happened about **1.46 seconds later**.

Conclusion

These are **two log records describing the same failed authentication attempt**, not two separate attacks.

The first records the **PAM authentication failure**.

The second records the **`su` failure**.

4. Counting Events

grep ... | wc -l

 `wc -l`

Means:

> Count the number of lines.

⚠️ Important:

> **Number of log lines ≠ number of attacks.**

Always inspect the events before deciding what they mean.


5. Extracting Information

FAILED SU (to root) h on pts/1

Result:

root

I used `sed` to extract it.

Important

the concept:

> **Extract the information I need from the log.**


6. Important `grep` Options

`-i`

Ignore uppercase/lowercase.


grep -i


`-a`

Treat the file as text.

grep -a

I needed this because our `auth.log` was being detected as a binary file.

`-E`

**Extended Regular Expressions**

the important use was:


grep -E "failed|failure"

Means:

> Find **failed OR failure**.

🧠 Remember:

> **E = Extended**

`-v`

Exclude matching lines.

grep -v "something"


Means:

> Remove lines containing `something`.

 `|`

Pipe.

command1 | command2

Means:

> Send the output of command 1 into command 2.


7. Three Important Authentication Attacks

Brute Force

**One account → many different passwords**

Example:

admin → password1 ❌
admin → password2 ❌
admin → password3 ❌
admin → password4 ❌

Easy memory:

> **ONE account + MANY passwords = BRUTE FORCE**


Password Spraying

**Many accounts → same password**

Example:

alice → Password123 ❌
bob → Password123 ❌
john → Password123 ❌
sara → Password123 ❌

Easy memory:

> **MANY accounts + SAME password = PASSWORD SPRAYING**


Credential Stuffing

The attacker uses **previously stolen credentials**.

Example:

alice : stolenPassword
bob : stolenPassword
john : stolenPassword

The attacker isn't necessarily guessing.

They're using credentials obtained from somewhere else.

Easy memory:

> **STOLEN credentials = CREDENTIAL STUFFING**


10. How to Recognize an Attack

Scenario A

admin → Password123 ❌
admin → Welcome1 ❌
admin → qwerty ❌
admin → letmein ❌

Answer:

> **Brute force** 

Because:

> Same account + different passwords.


Scenario B

alice → Password123 ❌
bob → Password123 ❌
john → Password123 ❌
sara → Password123 ❌
```

Answer:

> **Password spraying** 

Because:

> Different accounts + same password.


Scenario C

Previously stolen username/password combinations are being tried.

Answer:

> **Credential stuffing** ✅

Because:

> Previously stolen credentials are being reused.


Scenario D

user → wrong password 
user → correct password 

answer:
> **Not enough evidence to call it an attack.**

It could simply be a legitimate user making one mistake.


11. Successful Login After Failures

Example:

Failed ❌
Failed ❌
Failed ❌
Failed ❌
Failed ❌
Success ✅

This is important because:

> The attacker **might have eventually obtained the correct password**.

But we **do not automatically declare an attack**.

We investigate:

* Source IP
* Username
* Number of attempts
* Time period
* Successful login
* Other accounts targeted
* Whether the login was expected


12. SOC Mindset

Never think:

> "5 failed logins = attacker."

Instead:

Suspicious activity
       ↓
Investigate
       ↓
Check evidence
       ↓
Look for patterns
       ↓
Check context
       ↓
Make conclusion


Golden rule:

> **Suspicious ≠ Confirmed malicious**


memory:
grep      → find
-i        → ignore case
-a        → treat as text
-E        → extended patterns
-v        → exclude
|         → send output
wc -l     → count lines
sed       → extract/transform text

DAY 19 — ✅ COMPLETE**
