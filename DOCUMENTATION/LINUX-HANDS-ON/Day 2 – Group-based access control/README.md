# Linux Hands-On Practice – Day 2  
## Group Creation and User Assignment (Linux Level 1)

This repository documents my **Day 2 learning** as part of my **DevOps journey**, based on hands-on Linux tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of Day 2 was understanding and implementing **group-based access control**, which is a foundational concept in enterprise Linux environments.

---

## 📌 Task Overview

**Task Name:** Group Creation and User Assignment  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Servers:** All App Servers (`stapp01`, `stapp02`, `stapp03`)

### Task Requirements
- Create a group named `nautilus_sftp_users`
- Add user `jarod` to the group
- If the user does not exist, create it
- Perform the task on **all App Servers**

---

## 🏗 Infrastructure Context

This task follows a **multi-server enterprise architecture**:

Local Access  
↓  
Jump Host (jumphost)  
↓  
App Servers (stapp01 / stapp02 / stapp03)

Each App Server maintains its **own local user and group database**, so configuration must be applied **individually on every server**.

---

## 🔐 Access Details (Conceptual)

| Server | SSH User |
|------|----------|
| Jump Host | thor |
| App Servers | tony / steve / banner |

> 🔒 Direct root login is disabled. Administrative actions are performed using `sudo`.

---

## 🧠 Key Concepts Learned

- Why **group-based access control** is preferred over user-level permissions
- Difference between **primary** and **supplementary** groups
- Safe modification of user group memberships
- Risks of overwriting group assignments unintentionally
- Importance of **consistent configuration** across multiple servers
- Verification using authoritative system commands

---

## ⚙️ Commands Used

### Check if Group Exists
```bash
getent group nautilus_sftp_users
```
### Create Group (if missing)
```bash
sudo groupadd nautilus_sftp_users
```

### Check if User Exists
```bash
id jarod
```

### Create User (if missing)
```bash
sudo useradd jarod
```

### Add User to Group (Safe Method)
```bash
sudo usermod -aG nautilus_sftp_users jarod
```
```
-a ensures existing group memberships are preserved
-G specifies supplementary group assignment
```

## 🔍 Verification Steps
### Verify User and Group Membership
```bash
id jarod
```

### Expected output (example):
```
uid=1002(jarod) gid=1002(jarod) groups=1002(jarod),nautilus_sftp_users
```

## ❌ Mistakes Made & Learnings

### 1️⃣ Forgetting the -a Flag with usermod
```bash
usermod -G nautilus_sftp_users jarod
```
**Issue:**

- Overwrites all existing supplementary groups

- Can silently remove required access

**Learning:**

- Always use usermod -aG when adding users to groups

### 2️⃣ Assuming Changes on One Server Are Enough
**Issue:**

- Users and groups are local to each server

- Configuration drift occurs if changes aren’t repeated

**Learning:**

- Always apply identity changes on all required nodes

## 🧩 Key Takeaways

- Linux access control is group-centric by design

- Groups provide scalable and maintainable permission management

- Small command flags can have serious security implications

- Verification is mandatory, not optional

- Multi-server environments demand consistency

## 📚 Reference Documentation

- KodeKloud Nautilus Infrastructure Details
https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details

- Linux manual pages:
```bash
man groupadd
man usermod
man getent
```

## 🚀 DevOps Journey Progress

- ✅ Day 1 completed – User management fundamentals

- ✅ Day 2 completed – Group-based access control

- 📘 Focus: Linux identity & permission models

- 🎯 Goal: Build strong Linux foundations for DevOps roles

## 🤝 For Learners

If you are learning Linux administration:

- Think in terms of access models, not just commands

- Always verify system state before and after changes

- Treat identity management as a high-impact operation

- Feel free to fork, reuse, or suggest improvements.
---
⭐ If this repository helps you, consider starring it.
```