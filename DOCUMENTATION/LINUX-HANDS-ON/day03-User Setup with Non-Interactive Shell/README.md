# Linux Hands-On Practice – Day 3  
## Linux User Setup with Non-Interactive Shell (Linux Level 1)

This repository documents my **Day 3 learning** as part of my **DevOps journey**, based on hands-on Linux tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of Day 3 was creating a **non-interactive system user**, a common requirement for service accounts, backup agents, and automation tools in enterprise Linux environments.

---

## 📌 Task Overview

**Task Name:** Linux User Setup with Non-Interactive Shell  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 3 (`stapp03`)

### Task Requirements
- Create a user named `siva`
- Assign a **non-interactive shell**
- Perform the task on **App Server 3**

---

## 🏗 Infrastructure Context

This task follows an **enterprise access model**:

Local Access  
↓  
Jump Host (jumphost)  
↓  
App Server 3 (`stapp03`)

Service users are created with **restricted login capabilities** to reduce security risks.

---

## 🧠 Key Concepts Learned

- Difference between **interactive** and **non-interactive** users
- How Linux controls login access using the **login shell**
- Purpose of `/sbin/nologin` for service and automation accounts
- Why not all users should have shell access
- Importance of verification after user creation

---

## ⚙️ Commands Used

### Create User with Non-Interactive Shell
```bash
sudo useradd -s /sbin/nologin siva
```

### Explanation:

- useradd → creates the user

- -s /sbin/nologin → blocks interactive login

- siva → username

## 🔍 Verification Steps

### Verify User Entry
```bash
getent passwd siva
```

### Expected output (example):
```
siva:x:1003:1003::/home/siva:/sbin/nologin
```

### Key confirmation:
```
- User exists

- Login shell is /sbin/nologin
```


## 🧩 Key Takeaways

- Not all Linux users are meant for human login

- Non-interactive shells are essential for security hardening

- /sbin/nologin is preferred for service accounts

- Always verify user configuration using authoritative commands

## 📚 Reference Documentation

Linux manual pages:
```bash
man useradd
man getent
```

## 🤝 For Learners

If you are learning Linux:

- Don’t assume every user needs shell access

- Apply least privilege by default

- Always verify, even for simple tasks

Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```