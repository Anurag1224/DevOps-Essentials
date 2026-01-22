# Linux Hands-On Practice – Day 10  
## File Permission Correction using ACL (Linux Level 1)

This document captures **Day 10 learning** as part of my **DevOps hands-on journey**, based on real-world Linux security tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was correcting **misconfigured file permissions** using a combination of:
- Ownership (`chown`)
- Standard permissions (`chmod`)
- Access Control Lists (`setfacl`)

This mirrors how sensitive system files are protected in production environments.

---

## 📌 Task Overview

**Task Name:** File Permission Correction  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 2 (`stapp02`)  
**Target File:** `/etc/resolv.conf`

### Task Requirements

1. File owner must be `root`  
2. File group must be `root`  
3. Others should have **read only** permission  
4. User `james` must have **no permissions**  
5. User `jerome` should have **read only** permission  

---

## 🏗 Infrastructure Context

This task simulates a **security audit scenario** where a critical system file had incorrect permissions.

In real systems, such corrections are required to:
- Prevent unauthorized access
- Enforce least-privilege principles
- Protect configuration files from accidental changes

---

## 🧠 Key Concepts Learned

- Difference between **ownership and permissions**
- Understanding Linux permission model: user / group / others
- Using **ACL (Access Control Lists)** for per-user rules
- Why `chmod` alone is not sufficient for complex policies
- Verifying final access rules using `getfacl`

---

## ⚙️ Commands Used

### Step 1: Fix Ownership
```bash
sudo chown root:root /etc/resolv.conf
```

Ensures both owner and group are root.

Step 2: Set Base Permissions
sudo chmod 644 /etc/resolv.conf


Results in:

-rw-r--r--


Meaning:

Root → read & write

Group → read

Others → read

Step 3: Remove All Permissions for User james
sudo setfacl -m u:james:0 /etc/resolv.conf


Explicitly blocks james, even though others can read.

Step 4: Grant Read Only Permission to User jerome
sudo setfacl -m u:jerome:r /etc/resolv.conf


Allows jerome to read the file.

🔍 Verification Steps
Check Standard Permissions
ls -l /etc/resolv.conf


Expected output:

-rw-r--r--

Check ACL Rules
getfacl /etc/resolv.conf


Expected output includes:

user::rw-
user:james:---
user:jerome:r--
group::r--
other::r--


This confirms:

james → blocked

jerome → read only

Others → read only

❌ Common Mistakes & Learnings
1️⃣ Using chmod Instead of chown

chmod cannot change ownership

2️⃣ Forgetting ACL

Per-user rules cannot be implemented with chmod alone

3️⃣ Not Verifying with getfacl

ls -l does not show ACL entries

🧩 Key Takeaways

Ownership and permissions are separate concepts

ACL allows fine-grained, user-specific control

chmod sets general rules

setfacl sets exceptions

getfacl shows the final truth

📚 Reference Documentation

Linux manual pages:

man chown
man chmod
man setfacl
man getfacl


🤝 For Learners

If you are learning Linux security:

Always separate ownership from permissions

Use ACL when simple permissions are not enough

Never modify system files without verification

Think in terms of least privilege

Feel free to fork, reuse, or suggest improvements.

⭐ If this repository helps you, consider starring it.