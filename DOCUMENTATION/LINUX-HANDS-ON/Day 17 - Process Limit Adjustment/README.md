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
