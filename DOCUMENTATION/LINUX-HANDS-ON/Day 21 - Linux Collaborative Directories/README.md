# Linux Hands-On Practice – Day 21  
## Linux Collaborative Directories (Linux Level 2)

This document captures **Day 21 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was understanding how Linux supports **secure team collaboration** using:
- Group ownership  
- File permissions  
- The **SetGID bit**

This mirrors how shared directories are designed in production environments for teams like DevOps, SRE, and platform engineering.

---

## 📌 Task Overview

**Task Name:** Linux Collaborative Directories  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** App Server 3 (`stapp03`)  
**Target Path:** `/sysops/data`

### Task Requirements

- Create a directory `/sysops/data`
- Set the group owner to `sysops`
- Ensure all files inside inherit the `sysops` group
- User and group should have **read/write/execute**
- Others should have **no access**

---

## 🏗 Infrastructure Context

This task simulates a real-world scenario where multiple users from the same team need to **collaborate on shared data** while preventing access from other teams.

Such setups are commonly used for:
- Shared deployment directories  
- Log processing locations  
- Backup repositories  
- CI/CD workspaces  

---

## 🧠 Key Concepts Learned

- Difference between **creator’s group** and **directory’s group**
- Why normal permissions are not enough for collaboration
- Understanding **SetGID (Set Group ID)** on directories
- How Linux controls **group inheritance**
- Designing secure, team-based access models

---

## ⚙️ Commands Used

### Step 1: Connect to App Server 3
```bash
ssh banner@stapp03
hostname
```

Expected output:
```
stapp03
```

### Step 2: Create the Directory
```bash
sudo mkdir -p /sysops/data
```

### Step 3: Set Group Ownership
```bash
sudo chown :sysops /sysops/data
```

This ensures the directory belongs to the sysops team.

### Step 4: Set Permissions with SetGID

```bash
sudo chmod 2770 /sysops/data
```

Breakdown of 2770:
```
Digit	Meaning
2	SetGID (group inheritance)
7	Owner: rwx
7	Group: rwx
0	Others: no access
```
## 🔍 Verification Steps
```bash
ls -ld /sysops/data
```

Expected output:
```
drwxrws--- root sysops /sysops/data
```
The s in rws confirms SetGID is active.

## 🧩 Why SetGID Is Important

By default, Linux assigns new files to the creator’s primary group, not the directory’s group. This breaks collaboration in shared directories.

With SetGID:

- All new files automatically inherit the sysops group

- No manual permission fixes are required

- True team collaboration becomes possible

## ❌ Common Mistakes & Learnings

1️⃣ Using only chmod 770

- Does not enforce group inheritance

- New files may belong to wrong group

2️⃣ Forgetting SetGID

- Breaks collaboration silently

3️⃣ Using 777 permissions

- Creates a security risk

- Allows unauthorized access

## 🧩 Key Takeaways

- Collaboration is an ownership inheritance problem, not just an access problem

- SetGID is essential for shared team directories

- Group-based access is the Linux-native way to scale permissions

- Secure systems require both correct permissions and correct behavior

## 📚 Reference Documentation

Linux manual pages:
```bash
man chmod
man chown
man groups
```


## 🤝 For Learners

If you are learning Linux:

- Always understand default system behavior

- Don’t rely only on permissions

- Think in terms of teams, not individuals

- Design systems that are secure and maintainable

This task represents a core production Linux pattern used in real organizations.

```
⭐ If this repository helps you, consider starring it.
```