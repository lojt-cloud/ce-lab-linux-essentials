# Lab Solution: Linux Command Line Essentials
**Student Name: Balint Lojt
**Date: 10/07/2026 
**Environment Used:**  WSL

---

## Part 1: Environment Setup

### Connection Information

**Command used to connect:**

N/A    working with WSL

**Output of `whoami`:**

lojtb

**Output of `pwd`:**

/home/lojtb/cloud-engineering/ce-lab-linux-essentials

**Output of `uname -a`:**

Linux LojtLaptop 6.6.114.1-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Mon Dec  1 20:46:23 UTC 2025 x86_64 GNU/Linux


## Part 2: Navigation Practice

### Task: Navigate to /var/log and back

**Commands executed:**

# Navigate to /var/log
cd /var/log

# List contents
ls -l

# Return to home directory
cd ~


**Screenshot 1: /var/log directory listing**
<img width="1052" height="178" alt="01-var-log" src="https://github.com/user-attachments/assets/81664865-caeb-4e22-87d5-78c9a0db6ad6" />


---

## Part 3: Directory Structure Creation

### Project Structure

**Commands to create directory structure:**
```bash
# Create cloud-project directory

mkdir cloud-engineering

# Create nested directories

mkdir -p cloud-engineering/ce-lab-linux-essentials


# Create files

touch README.md
echo "additional line to README" > README.md
touch cloud-engineering/ce-lab-linux-essentials/README.md


```

**Screenshot 2: Project structure (tree or ls -R output)**
<img width="641" height="117" alt="02-project-structure" src="https://github.com/user-attachments/assets/9dac944e-4a62-4d31-9754-5914cac44370" />



## Part 4: File Operations

### Copy, Move, Delete Practice

**Commands for test directory task:**
```bash

# Create test directory with files
mkdir test-directory
touch testfile-1 testfile-2 testfile-3 testfile-4 testfile-5

# Make backup copy
cp -r test-directory test-directory-backup

# Rename backup
mv test-directory-backup test-directory-backup-renamed

# Delete backup
rm -r test-directory-backup-renamed

# Verify final state

ls test-directory
testfile-1  testfile-2  testfile-3  testfile-4  testfile-5
lojtb@LojtLaptop:~$ ls test-directory-backup-renamed
ls: cannot access 'test-directory-backup-renamed': No such file or directory

**Screenshot 3: File operations results**
<img width="783" height="140" alt="03-file-operations" src="https://github.com/user-attachments/assets/2d152872-5790-4326-a44c-752e0e1f4ac6" />



## Part 5: Viewing File Contents

### Log File Analysis

**Output of last 3 lines:**


2026-01-14 08:15:30 INFO Backup completed successfully
2026-01-14 08:20:00 DEBUG Garbage collection triggered
2026-01-14 08:25:15 INFO Health check: OK

**Command used:**

tail -n 3 app/logs/application.log


## Part 6: Searching with grep

### Task: Search log file

**1. Count ERROR messages:**
```bash
# Command:

grep -c "ERROR" app/logs/application.log

# Output:
2

**2. Find WARNING messages with line numbers:**
```bash
# Command:

grep -n "WARNING" app/logs/application.log

# Output:

5:2026-01-14 08:02:45 WARNING Database connection slow
11:2026-01-14 08:08:45 WARNING Memory usage at 85%

**3. Extract user login events:**
```bash
# Command:
grep "login" app/logs/application.log

# Output:
2026-01-14 08:01:23 INFO User login: alice@example.com
2026-01-14 08:03:12 INFO User login: bob@example.com

**Screenshot 4: grep search results**
<img width="632" height="292" alt="04-grep-results" src="https://github.com/user-attachments/assets/30bbc252-6fbe-4178-b403-b3952e662042" />


---

## Part 7: File Permissions

### Task: Create and secure script

**Commands executed:**
```bash
# Create test script

touch test.sh

# Check initial permissions

ls -l test.sh

# Make executable for owner only

chmod 700 test.sh

# Verify permissions

ls -l test.sh

**Initial permissions:** -rw-r--r-- 1 lojtb lojtb 0 Jul 10 12:34 test.sh

**Final permissions:** -rwx------ 1 lojtb lojtb 0 Jul 10 10:18 test.sh

**Screenshot 5: Permission changes**
<img width="679" height="101" alt="05-permissions" src="https://github.com/user-attachments/assets/97ec7d5d-7b9d-48dc-b7c8-66dce921d5fa" />


### Secure Backup Script

**Script content:**

#!/bin/bash
echo "Starting backup..."
cp -r app app-backup-$(date +%Y%m%d)
echo "Backup completed."

**Permissions set:**
```bash
# Command:chmod 700 backup.sh

# Result (ls -l):
-rwx------ 1 lojtb lojtb 100 Jul 10 10:30 backup.sh


## Part 8: Pipes and Redirects

### Task: Command chaining

**1. Count total lines in all .log files:**
```bash
# Command:
find . -name "*.log" -exec wc -l {} +
# Result:
15 ./app/logs/application.log
  2 ./test.log
  1 ./output.log
  1 ./error.log
  1 ./combined.log
 20 total

**2. Find unique log levels and count:**
```bash
# Command:
cat app/logs/application.log | awk '{print $3}' | sort | uniq -c
# Result:
2 DEBUG
      2 ERROR
      9 INFO
      2 WARNING

**3. List files sorted by size:**
```bash
# Command:

ls -lhS

# Result:

total 24K
drwxr-xr-x 5 lojtb lojtb 4.0K Jul 10 10:46 app
drwxr-xr-x 3 lojtb lojtb 4.0K Jul 10 10:49 scripts
-rw-r--r-- 1 lojtb lojtb   60 Jul 10 11:18 output.log
-rw-r--r-- 1 lojtb lojtb   60 Jul 10 11:17 error.log
-rw-r--r-- 1 lojtb lojtb   60 Jul 10 11:18 combined.log
-rw-r--r-- 1 lojtb lojtb   24 Jul 10 11:17 test.log

**Screenshot 6: Pipes and redirects output**
<img width="925" height="92" alt="06-pipes-redirects" src="https://github.com/user-attachments/assets/e9795172-8789-4c47-b735-64c602c62ad8" />


---

## Part 9: Process Management

### Task: Background process

**1. Start long-running command in background:**
```bash
# Command:

sleep 300 &

# Output (job number):

[1] 20706

**2. List all jobs:**
```bash
# Command:

 jobs

# Output:
[1]+  Running                    sleep 300 &

**3. Kill the process:**
```bash
# Command:
kill %1
# Verification:
jobs 
lojtb@LojtLaptop:~/cloud-project$      (gave back an empty output, which means there are no running tasks)

**Screenshot 7: Process management**
<img width="480" height="178" alt="07-processes" src="https://github.com/user-attachments/assets/39fc9d18-ce3c-49d5-bb8f-d3396a677a0d" />


---

## Part 10: Cloud Engineering Scenarios

### CloudTrail Log Analysis

**1. Events per user:**
```bash
# Command:

grep -o '"userName":"[^"]*"' ~/aws-logs/cloudtrail.json | sort | uniq -c

# Result:

 2 "userName":"alice"
 1 "userName":"bob"
 2 "userName":"charlie"

**2. EC2 operations:**
```bash
# Command:

grep "EC2" ~/aws-logs/cloudtrail.json

# Result:
- RunInstances (by charlie, instance i-1234567890)
- TerminateInstances (by charlie, instance i-0987654321)

{"eventTime":"2026-01-14T08:15:00Z","eventName":"RunInstances","userIdentity":{"userName":"charlie"},"resources":[{"type":"AWS::EC2::Instance","name":"i-1234567890"}]}
{"eventTime":"2026-01-14T08:20:00Z","eventName":"TerminateInstances","userIdentity":{"userName":"charlie"},"resources":[{"type":"AWS::EC2::Instance","name":"i-0987654321"}]}



**3. Unique event types:**
```bash
# Command:

grep -o '"eventName":"[^"]*"' ~/aws-logs/cloudtrail.json | cut -d'"' -f4 | sort | uniq

# Result:
CreateBucket
DeleteBucket
PutObject
RunInstances
TerminateInstances

**Screenshot 8: CloudTrail analysis**
<img width="1104" height="336" alt="08-cloudtrail-analysis" src="https://github.com/user-attachments/assets/fee8e32e-0b5b-4f09-8fc6-040c0f958b23" />


### System Monitoring

**1. Disk space:**
```bash
# Command: df -h

It gave back too many lines, and I found it hard to dig out what I needed to find, so I looked up how to narrow it down.
df -h /
The "/" narrows down to only show me the filesystem containing this specific path. 

# Total space:1007G
# Used: 2.5G
# Available: 954G
# Usage %: 1%
```

**2. Available memory:**
```bash
# Command: free -h


# Total: 7.6Gi 
# Used: 674Mi
# Free: 6.8Gi
```

**3. CPU cores:**
```bash
# Command: lscpu

Again, as before, I had too many lines, so I found an easier piped option:
lscpu | grep -E "^CPU\(s\)|Model name"

What it does: Show me any line that starts with CPU(s), or any line that contains Model name, anywhere in the file.
This one feels over my level for now, but in the future, I can see the use of it.
# CPU(s): 12
# Model: 12th Gen Intel(R) Core(TM) i5-1245U
```

**Screenshot 9: System resources**
<img width="894" height="242" alt="09-system-resources" src="https://github.com/user-attachments/assets/c1a075d3-42ae-4f7d-8188-d6ad4156a5ce" />


---

## Command Cheat Sheet (Your Most Used)

**List your 10 most-used commands from this lab:**

1. ls -l / ls -la / ls -lh (for listing files with different details)
2. cd / pwd (moving around in directories + checking where I am)
3. mkdir -p (to create directories with a nested path)
4. cat (puts out what's inside a file)
5. grep (specific search inside files with different criteria (-n,-c,-o))
6. chmod (changing the permissions of who can do what, and it is important for security)
7. cp / mv / rm  (to copy files, move, remove depending on what follows (-r))
8. | (pipe is to chain commands together)
9. sort / uniq -c (the counting/deduplication pattern for analysing logs and lists)
10. ps aux / jobs / kill (process management, right now didn't do much for me because I haven't used it in actual services)

---

## Reflection Questions

### 1. How do file permissions enhance security in cloud environments?

File permissions enhance security by only letting the people who actually 
need access get it, and locking everyone else out - same idea as least
privilege in IAM. I did this today with a config file holding a database
password, setting it to chmod 600 so only the owner could read or write it,
nobody else on the system could touch it at all.

Without that, sensitive stuff like passwords or scripts could be read or
messed with by any other user on the system, which is a real risk on shared
servers or cloud instances.

### 2. Why is piping commands together more efficient than intermediate files?

Piping skips having to save each step's output to a temporary file just to
feed it into the next command. Without pipes, I'd have to run grep, save the
result to a file, then run wc -l on that file, then remember to delete the
leftover file after. With a pipe, the output of one command goes straight
into the next one in memory, no extra files created or cleaned up.

It also lets me chain simple commands together to get a result none of them
could produce alone. like counting the most common log level in one line
instead of several separate steps.

### 3. Describe a real-world scenario where you'd use `tail -f`.

tail -f is for watching a log file live, as new lines get added, instead of
just checking a snapshot once. A real scenario: if I'm deploying a new app
version, I'd run tail -f on the application log so I can watch for errors
the moment they happen, rather than manually re-checking the file over and
over to see if something new shows up.

### 4. What's the difference between killing with `kill` vs `kill -9`?

The plain "kill" command sends a request to stop the running process, but it
doesn't stop it immediately - it finishes up what it's doing first, cleaning
everything up (closing open files, saving data) before closing. "kill -9"
forcefully closes everything without any saving, instantly killing it. "-9"
is a dangerous command, so I'd only use it as a last resort if the normal
kill command doesn't work.

### 5. How does Linux CLI proficiency help with AWS CLI usage?

AWS CLI's syntax and behaviour are built around Linux/Unix conventions - flags,
piping output into other tools like grep, redirecting output to files, etc.
So the skills transfer directly: knowing how to navigate, search, and chain
commands on Linux makes AWS CLI feel familiar rather than like learning a
whole new way of working.

Also, the vast majority of servers (and most cloud infrastructure) run on
Linux, so this isn't just about AWS CLI specifically - it's a foundational
skill for basically anything in cloud/DevOps work.


## Troubleshooting Log

**Did you encounter any issues?** 
No

**If yes, document:**

| Issue | Commands Tried | Solution | Time Spent |
|-------|---------------|----------|------------|
|       |               |          |            |
|       |               |          |            |
|       |               |          |            |

---

## Cleanup Confirmation
not executed - keeping files to revisit later
- [] Removed ~/cloud-project directory
- [] Removed ~/aws-logs directory
- [] Verified no leftover files

**Cleanup commands:**
If I didn't keep the files, I would execute these: 

cd ~
rm -rf cloud-project
rm -rf aws-logs

## Self-Assessment

**Rate your confidence (1-5, where 5 is expert):**

| Skill | Before Lab | After Lab | Notes |
|-------|-----------|-----------|-------|
| Filesystem navigation | 4/5 | 4,5/5 | The basic navigation itself doesn't feel like an issue |
| File manipulation | 3/5 | 4/5 |Some path confusion (files landing in wrong folders) but self-corrected each time without help |
| Viewing/searching files | 3/5 | 4/5 |grep + flags with it is understandable, can get confusing when using pipes with it |
| File permissions | 3/5 | 4/5 |Applied chmod 600/700/750 correctly multiple times, understand the r/w/x math, not just copying numbers |
| Pipes and redirects | 2/5 | 3/5 | Needed real walkthrough on sort -h vs -n and multi-stage chains, but executed every task correctly once explained - still building intuition here|
| Process management | 3/5 | 3,5/5 |knows the commands, hasn't yet had to actually use them for their real purpose |
| Log analysis | 2/5 | 3/5 |CloudTrail JSON extraction with grep -o worked correctly, understood what each piece of the pattern was doing  |

---

## Bonus Challenges Completed
N/A
- [ ] Explored `awk` for text processing
- [ ] Created a shell script with multiple commands
- [ ] Used `find` with complex criteria
- [ ] Practiced `sed` for text replacement
- [ ] Set up custom bash aliases

**Bonus notes:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

---

## Instructor Verification

**Instructor Name:** ___________________________

**Date Reviewed:** ___________________________

**All tasks completed:** ☐ Yes ☐ No

**Comments:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

**Grade/Status:** ___________________________

---

**Lab Status:** ☐ Complete ☐ Needs Revision

**Total Time Spent:** ________ minutes

**Submission Date:** ___________________________
