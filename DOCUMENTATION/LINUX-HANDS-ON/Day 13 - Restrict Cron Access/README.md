# Linux Hands-On Practice – Day 13  
## Restrict Cron Access (Linux Level 1)

This document captures **Day 13 learning** as part of my **DevOps hands-on journey**, based on real-world Linux security and automation control tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was **restricting access to cron**, ensuring that only approved users are allowed to schedule automated jobs.

This mirrors how automation is controlled in production environments to prevent misuse and security risks.

---

## 📌 Task Overview

**Task Name:** Configure crontab access  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 2 (`stapp02`)  

### Task Requirements

- Allow crontab access to user `mariyam`  
- Deny crontab access to user `ryan`  

---

## 🏗 Infrastructure Context

In enterprise systems, automation is extremely powerful.  
Cron jobs can:

- Run scripts automatically  
- Modify files  
- Transfer data  
- Execute commands without human interaction  

If unrestricted, cron becomes a **major security risk**.

Therefore, organizations restrict cron usage to only **trusted users**.

---

## 🧠 Key Concepts Learned

- Understanding what cron and crontab are  
- Why automation must be access-controlled  
- Using allow/deny lists for system features  
- Testing permissions by switching users  
- Relating cron security to RBAC in modern tools  

---

## ⚙️ Commands Used

### Step 1: Login to App Server 2
```bash
ssh steve@stapp02
hostname
```Expected output:

stapp02

Step 2: Allow Only mariyam to Use Cron
sudo vi /etc/cron.allow


Add:

mariyam


This ensures only users listed here can use crontab.

Step 3: Explicitly Deny ryan
sudo vi /etc/cron.deny


Add:

ryan

🔍 Verification Steps
Test as mariyam (Should Work)
su - mariyam
crontab -e


User should be allowed to edit cron jobs.

Test as ryan (Should Fail)
su - ryan
crontab -e


Expected output:

You (ryan) are not allowed to use this program (crontab)

❌ Common Mistakes & Learnings
1️⃣ Editing Only cron.deny

Deny list is weaker than allow list

2️⃣ Forgetting to Use sudo

System files require root privileges

3️⃣ Testing as Root

Root is always allowed, so test must be done as real users

4️⃣ Not Verifying Access

Always confirm behavior with crontab -e

🧩 Key Takeaways

Automation is powerful and must be restricted

Cron access should follow a whitelist model

cron.allow is more secure than cron.deny

Testing must be done under actual user identities

This concept applies to all automation systems

📚 Reference Documentation

Linux manual pages:

man cron
man crontab

🚀 DevOps Journey Progress

✅ Day 1 – Custom user creation

✅ Day 2 – Group-based access control

✅ Day 3 – Non-interactive users

✅ Day 4 – Service user without home directory

✅ Day 5 – Temporary user with expiry date

✅ Day 6 – Ownership-based file filtering

✅ Day 7 – Secure SSH access

✅ Day 8 – Data archiving and transfer

✅ Day 9 – Script execution permissions

✅ Day 10 – File permission correction with ACL

✅ Day 11 – String replacement with sed

✅ Day 12 – Secure data transfer with scp

✅ Day 13 – Controlled cron access

📘 Focus: Linux security & automation governance
🎯 Goal: Strong operational Linux foundation for DevOps roles

🤝 For Learners

If you are learning Linux automation:

Never allow automation tools without access control

Always test permissions as the actual user

Prefer allow lists over deny lists

Treat automation as a security-sensitive feature

Feel free to fork, reuse, or suggest improvements.

⭐ If this repository helps you, consider starring it.