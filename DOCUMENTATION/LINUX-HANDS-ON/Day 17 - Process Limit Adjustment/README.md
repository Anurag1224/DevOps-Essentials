# Linux Hands-On Practice – Day 17  
## Process Limit Adjustment (Linux Level 1)

This document captures **Day 17 learning** as part of my **DevOps hands-on journey**, based on real-world Linux performance and resource management tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was enforcing **process limits for a specific user** to prevent performance degradation and protect overall system stability.

This reflects how resource control is applied in production environments to avoid misuse and runaway processes.

---

## 📌 Task Overview

**Task Name:** Process Limit Adjustment  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** Storage Server (`ststor01`)  

### Task Requirements

For user `nfsuser`:

- Set **soft limit** for maximum processes to `1024`  
- Set **hard limit** for maximum processes to `2026`  

---

## 🏗 Infrastructure Context

In multi-user Linux systems, each user can spawn multiple processes such as:

- Shell sessions  
- Background jobs  
- Services  
- Scripts  

If a single user creates too many processes:
- CPU usage increases  
- Memory gets exhausted  
- The system becomes slow or unresponsive  

To avoid this, Linux provides a mechanism to enforce **per-user resource limits**.

This task simulates a real operational scenario where a specific user is causing performance issues and needs controlled limits.

---

## 🧠 Key Concepts Learned

- What processes are in Linux  
- Difference between **soft** and **hard** limits  
- Using `nproc` to control number of processes  
- Where Linux stores resource limits  
- How limits help protect system stability  

---

## ⚙️ Commands Used

### Step 1: Login to Storage Server
```bash
ssh natasha@ststor01
hostname
```
Expected output:
```
ststor01
```
### Step 2: Edit Process Limits Configuration
```bash
sudo vi /etc/security/limits.conf
```

Add the following lines at the bottom:
```bash
nfsuser soft nproc 1024
nfsuser hard nproc 2026
```

Explanation:

- nfsuser → user to apply limits

- soft → warning limit

- hard → absolute maximum

- nproc → number of processes

## 🔍 Verification Steps (Optional)

Switch to the user:
```bash
su - nfsuser
```

Check soft limit:
```bash
ulimit -u
```

Expected output:
```
1024
```

Check hard limit:
```bash
ulimit -Hu
```

Expected output:
```
2026
```

**Note:** Limits apply on the next login session for the user.

## ❌ Common Mistakes & Learnings

1️⃣ Editing the Wrong Server

- Must be applied on the Storage Server

2️⃣ Typos in Username

- Limits won’t apply if username is incorrect

3️⃣ Confusing Soft and Hard Limits

- Soft can be adjusted by user (within hard)

Hard cannot be exceeded

4️⃣ Expecting Immediate Effect

- User must re-login for limits to apply

## 🧩 Key Takeaways

- Process limits protect system performance

- One user should never be allowed unlimited resources

- Soft and hard limits provide layered control

- Resource management is part of system security

- Stability comes from enforcing boundaries, not just scaling

## 📚 Reference Documentation

Linux manual pages:
```bash
man limits.conf
man ulimit
```

🤝 For Learners

If you are learning Linux system administration:

- Monitor how users consume resources

- Always apply limits for critical services

- Test limits in controlled environments

- Understand that stability comes from prevention, not reaction

Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```