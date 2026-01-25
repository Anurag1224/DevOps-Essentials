# Linux Hands-On Practice – Day 12  
## Secure Data Transfer using SCP (Linux Level 1)

This document captures **Day 12 learning** as part of my **DevOps hands-on journey**, based on real-world Linux secure data transfer tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was transferring a **confidential file securely between servers** using standard Linux networking tools.

This mirrors how sensitive data is moved in production environments where direct access to servers is restricted.

---

## 📌 Task Overview

**Task Name:** Secure Data Transfer  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Source Server:** Jump Host  
**Destination Server:** App Server 3 (`stapp03`)  
**Source File:** `/tmp/nautilus.txt.gpg`  
**Destination Path:** `/home/web/`

### Task Requirements

- Locate the encrypted file on the Jump Host  
- Transfer it securely to App Server 3  
- Place it inside `/home/web` directory  
- Ensure data is not modified during transfer  

---

## 🏗 Infrastructure Context

In enterprise environments, developers often do not have **direct access** to application servers.

Instead, a **Jump Host (bastion server)** is used as an intermediate system:

User → Jump Host → App Server


This architecture:
- Improves security  
- Limits attack surface  
- Allows auditing of access  

System administrators act as the **controlled bridge** between systems.

---

## 🧠 Key Concepts Learned

- Difference between local and remote file operations  
- Understanding why `cp` cannot copy across servers  
- Using `scp` for encrypted file transfer over SSH  
- Verifying data at both source and destination  
- Role of Jump Hosts in secure infrastructures  

---

## ⚙️ Commands Used

### Step 1: Verify Source File Exists (on Jump Host)
```bash
ls -l /tmp/nautilus.txt.gpg

Step 2: Transfer File to App Server 3
scp /tmp/nautilus.txt.gpg banner@stapp03:/home/web/


This command:

Uses SSH for encryption

Copies file across servers

Preserves file integrity

🔍 Verification Steps
Login to App Server 3
ssh banner@stapp03

Verify File Exists at Destination
ls -l /home/web/nautilus.txt.gpg

Optional: Verify File Size

On Jump Host:

ls -lh /tmp/nautilus.txt.gpg


On App Server 3:

ls -lh /home/web/nautilus.txt.gpg


File sizes should match.

❌ Common Mistakes & Learnings
1️⃣ Using cp Instead of scp

cp works only on the same machine

Cannot transfer across servers

2️⃣ Running scp from the Wrong Server

Must be executed on the source server

3️⃣ Using Wrong Destination Path

File must be placed exactly in /home/web/

4️⃣ Forgetting to Verify Transfer

Always confirm on destination

🧩 Key Takeaways

Secure file transfer is a core system admin task

Jump Hosts are standard in enterprise security

scp is the simplest encrypted transfer tool

Verification is mandatory for sensitive data

Access control matters more than convenience

📚 Reference Documentation

Linux manual pages:

man scp
man ssh

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

📘 Focus: Linux networking & secure operations
🎯 Goal: Strong operational Linux foundation for DevOps roles

🤝 For Learners

If you are learning Linux system administration:

Understand network boundaries

Always verify both ends of a transfer

Never move sensitive data without encryption

Think in terms of security-first workflows

Feel free to fork, reuse, or suggest improvements.

⭐ If this repository helps you, consider starring it.