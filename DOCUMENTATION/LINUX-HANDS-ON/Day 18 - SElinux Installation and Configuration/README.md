# Linux Hands-On Practice – Day 18  
## SELinux Installation and Configuration (Linux Level 1)

This document captures **Day 18 learning** as part of my **DevOps hands-on journey**, based on real-world Linux security configuration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was understanding how **SELinux (Security-Enhanced Linux)** is installed, how its behavior is controlled, and how to permanently disable it at boot time for staged security rollout.

This reflects how security features are introduced and managed carefully in real production environments.

---

## 📌 Task Overview

**Task Name:** SELinux Installation and Configuration  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 2 (`stapp02`)  

### Task Requirements

- Install the required SELinux packages  
- Permanently disable SELinux  
- Do not reboot the server  
- Ignore current runtime status  
- Final state after reboot should be **disabled**

---

## 🏗 Infrastructure Context

SELinux is a **mandatory access control (MAC)** system that adds an extra layer of security on top of traditional Linux permissions.

Even if:
- file permissions allow access  
- user has correct rights  

SELinux can still **block actions** based on security policies.

In real enterprises, SELinux is widely used to:
- contain breaches  
- restrict compromised services  
- enforce security policies  
- meet compliance requirements  

However, enabling SELinux without preparation can break applications.  
Therefore, organizations often **install it first, configure policies, and enable it later**.

This task simulates that staged security approach.

---

## 🧠 Key Concepts Learned

- Difference between DAC (traditional permissions) and MAC (SELinux)  
- Runtime vs persistent SELinux configuration  
- Importance of staging security features  
- Why security changes should not be rushed in production  
- How system configuration files control boot-time behavior  

---

## ⚙️ Commands Used

### Step 1: Login to App Server 2
```bash
ssh steve@stapp02
hostname
```

Expected output:
```
stapp02
```
### Step 2: Install SELinux Packages

Since the system is RHEL-based, use yum:
```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```

This installs:

- Core SELinux engine

- Default targeted policies

- Management utilities

### Step 3: Permanently Disable SELinux

Edit the configuration file:

```bash
sudo vi /etc/selinux/config
```

Change this line:
```
SELINUX=enforcing
```

To:
```
SELINUX=disabled
```

Save and exit.

## 🔍 Important Notes

- Do not add a new line; modify the existing one

- No reboot is required for this task

- The change will take effect after the next reboot

- Commands like setenforce are temporary and not used here

- Runtime status (getenforce) can be ignored as per task instructions

## ❌ Common Mistakes & Learnings

1️⃣ Using setenforce 0

- Only changes current session

- Does not persist after reboot

2️⃣ Adding a New SELINUX=disabled Line

Creates conflicting entries

- System may still boot in enforcing mode

3️⃣ Rebooting the Server

- Not required and not allowed in this task

4️⃣ Editing the Wrong Server

- Must be done only on App Server 2

## 🧩 Key Takeaways

- SELinux adds a powerful mandatory security layer

- Permanent behavior is controlled via /etc/selinux/config

- Runtime and boot-time configuration are different concepts

- Security features should be rolled out gradually

- Configuration discipline is critical in production systems

## 📚 Reference Documentation

Linux manual pages:
```
man selinux
man getenforce
man setenforce
```

## 🤝 For Learners

If you are learning Linux security:

- Understand before enabling security layers

- Never blindly enforce SELinux in production

- Always distinguish between runtime and persistent config

- Treat security changes as high-impact operations

- Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```