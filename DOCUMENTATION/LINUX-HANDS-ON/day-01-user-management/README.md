# Linux Hands-On Practice – Day 1  
## Custom Apache User Setup (Linux Level 1)

This repository documents my **Day 1 learning** as part of my **DevOps journey**, based on hands-on Linux tasks from the **KodeKloud Engineer – Nautilus Project**.

The purpose of this repository is to:
- Capture **practical Linux learnings**
- Document **mistakes and corrections**
- Act as a **revision reference**
- Help **other learners** understand real-world Linux administration concepts

---

## 📌 Task Overview

**Task Name:** Custom Apache User Setup  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 3 (`stapp03`)

### Task Requirements
- Create a user named `john`
- Assign a custom UID: `1699`
- Set the home directory to `/var/www/john`
- Perform the task on **App Server 3**

---

## 🏗 Infrastructure Context

This task follows an **enterprise-style access architecture**:

Local Access
↓
Jump Host (jumphost)
↓
App Server 3 (stapp03)


Direct access to application servers is restricted.  
All connections are routed through a **Jump Host**, similar to real production environments.

---

## 🔐 Access Details (Conceptual)

| Server | SSH User |
|--------|----------|
| Jump Host | thor |
| App Server 3 | banner |

> 🔒 Direct root login is disabled. Administrative tasks are performed using `sudo`.

---

## 🧠 Key Concepts Learned

- Difference between **server identity** and **user identity**
- Importance of verifying the **correct server** before making changes
- Creating Linux users with **custom UID and home directory**
- Enterprise-safe verification using `getent`
- Difference between `useradd` and `adduser`
- How to handle partial or incorrect configurations safely

---

## ⚙️ Commands Used

#### Connect to App Server 3
```bash
ssh banner@stapp03
```
#### Verify Correct Server
```
hostname
```

#### Expected output:
```
stapp03
```
#### Create User with Custom UID and Home Directory
```
sudo useradd -u 1699 -d /var/www/john -m john
```
## 🔍 Verification Steps
#### Verify User ID
```
id john
```

#### Expected output:
```
uid=1699(john)
```

#### Verify User Entry (Authoritative Source)
```
getent passwd john
```

#### Expected output:
```
john:x:1699:1699::/var/www/john:/bin/bash
```

#### Verify Home Directory
```
ls -ld /var/www/john
```

## ❌ Mistakes Made & Learnings

### 1️⃣ Using adduser Instead of useradd
```
sudo adduser -u 1699 -d /var/www/john -m john
```

#### Issue:

- adduser is a high-level, interactive wrapper

- Flags may behave inconsistently across distributions

- Not ideal for exams or automation

#### Learning:

- Prefer useradd for precision and predictability

### 2️⃣ Attempting to Recreate an Existing User
```
useradd: user 'john' already exists
```


#### Learning:

- useradd creates users only

- Existing users must be inspected or modified carefully

- Always verify system state before fixing issues

## 🧩 Key Takeaways

- Always verify:

    - Which server you are on (hostname)

    - Which user you are logged in as (whoami)

- Use useradd for professional and exam-ready workflows

- Use getent instead of directly reading /etc/passwd

- Datacenter and environment context comes from documentation, not Linux commands

## 📚 Reference Documentation

- KodeKloud Nautilus Infrastructure Details
https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details

- Linux manual pages:
```
man useradd
man getent
```

## 🚀 DevOps Journey Progress

    - ✅ Day 1 completed

    - 📘 Focus: Linux fundamentals & enterprise access patterns

    - 🎯 Goal: Build a strong foundation for DevOps and cloud-native roles

## 🤝 For Learners

If you are starting with Linux:

- Don’t rush commands

- Understand why before how

- Mistakes are part of the learning process

Feel free to fork, reuse, or suggest improvements.
```
⭐ If this repository helps you, consider starring it.
``` 