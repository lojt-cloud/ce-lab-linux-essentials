# Lab Solution: Linux Command Line Essentials
**Student Name: Balint Lojt
**Date: 10/07/2026 
**Environment Used:**  EC2

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

# Result:
_____________________________________________________________
```

**2. Find unique log levels and count:**
```bash
# Command:

# Result:
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

**3. List files sorted by size:**
```bash
# Command:

# Result:
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

**Screenshot 6: Pipes and redirects output**
![Pipes output](screenshots/06-pipes-redirects.png)

---

## Part 9: Process Management

### Task: Background process

**1. Start long-running command in background:**
```bash
# Command:

# Output (job number):
_____________________________________________________________
```

**2. List all jobs:**
```bash
# Command:

# Output:
_____________________________________________________________
```

**3. Kill the process:**
```bash
# Command:

# Verification:
_____________________________________________________________
```

**Screenshot 7: Process management**
![Processes](screenshots/07-processes.png)

---

## Part 10: Cloud Engineering Scenarios

### CloudTrail Log Analysis

**1. Events per user:**
```bash
# Command:

# Result:
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

**2. EC2 operations:**
```bash
# Command:

# Result:
_____________________________________________________________
_____________________________________________________________
```

**3. Unique event types:**
```bash
# Command:

# Result:
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

**Screenshot 8: CloudTrail analysis**
![CloudTrail](screenshots/08-cloudtrail-analysis.png)

### System Monitoring

**1. Disk space:**
```bash
# Command: df -h

# Total space: _______________ 
# Used: _______________
# Available: _______________
# Usage %: _______________%
```

**2. Available memory:**
```bash
# Command: free -h

# Total: _______________
# Used: _______________
# Free: _______________
```

**3. CPU cores:**
```bash
# Command: lscpu

# CPU(s): _______________
# Model: _______________
```

**Screenshot 9: System resources**
![System resources](screenshots/09-system-resources.png)

---

## Command Cheat Sheet (Your Most Used)

**List your 10 most-used commands from this lab:**

1. _______________________________________________
2. _______________________________________________
3. _______________________________________________
4. _______________________________________________
5. _______________________________________________
6. _______________________________________________
7. _______________________________________________
8. _______________________________________________
9. _______________________________________________
10. _______________________________________________

---

## Reflection Questions

### 1. How do file permissions enhance security in cloud environments?

**Your answer:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

### 2. Why is piping commands together more efficient than intermediate files?

**Your answer:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

### 3. Describe a real-world scenario where you'd use `tail -f`.

**Your answer:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

### 4. What's the difference between killing with `kill` vs `kill -9`?

**Your answer:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

### 5. How does Linux CLI proficiency help with AWS CLI usage?

**Your answer:**
```
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
_____________________________________________________________
```

---

## Troubleshooting Log

**Did you encounter any issues?** (Yes/No): ______

**If yes, document:**

| Issue | Commands Tried | Solution | Time Spent |
|-------|---------------|----------|------------|
|       |               |          |            |
|       |               |          |            |
|       |               |          |            |

---

## Cleanup Confirmation

- [ ] Removed ~/cloud-project directory
- [ ] Removed ~/aws-logs directory
- [ ] Verified no leftover files

**Cleanup commands:**
```bash
_____________________________________________________________
_____________________________________________________________
```

---

## Self-Assessment

**Rate your confidence (1-5, where 5 is expert):**

| Skill | Before Lab | After Lab | Notes |
|-------|-----------|-----------|-------|
| Filesystem navigation | ___/5 | ___/5 | |
| File manipulation | ___/5 | ___/5 | |
| Viewing/searching files | ___/5 | ___/5 | |
| File permissions | ___/5 | ___/5 | |
| Pipes and redirects | ___/5 | ___/5 | |
| Process management | ___/5 | ___/5 | |
| Log analysis | ___/5 | ___/5 | |

---

## Bonus Challenges Completed

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
