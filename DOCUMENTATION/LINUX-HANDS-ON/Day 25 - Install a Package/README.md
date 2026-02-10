# Linux Hands-On Practice – Day 25  
## Installing Packages (zip) – Linux Level 2

This document captures **Day 25 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was installing required packages consistently across multiple servers to meet application requirements.

---

## 📌 Task Overview

**Task Name:** Install a Package  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Servers:**
- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

Install the **zip** package on all application servers.

---

## 🏗 Infrastructure Context

Applications often depend on system utilities and libraries.  
Missing packages can lead to:
- Deployment failures
- Script errors
- Backup or compression failures

Ensuring required packages are installed across all nodes is a basic but critical operational task.

---

## 🧠 Key Concepts Learned

- Using package managers to install software
- Verifying package installation
- Importance of consistency across servers
- Understanding dependencies in Linux environments

---

## ⚙️ Commands Used

### Step 1: Connect to Server
```bash
ssh tony@stapp01
hostname
```

Repeat on all app servers.

Step 2: Install zip Package
```bash
sudo yum install -y zip
```

Explanation:

- yum → Package manager

- install → Install software

- -y → Auto-confirm prompts

Step 3: Verify Installation
```bash
zip -v
```

Or:
```bash
rpm -qa | grep zip
```

## 🔍 Verification Steps

- Confirm package installation

- Ensure installation is completed on all app servers

- Verify command availability

## ❌ Common Mistakes & Learnings

1️⃣ Installing on only one server
- Each server maintains its own package database.

2️⃣ Forgetting verification
- Always confirm installation.

3️⃣ Running commands without confirming hostname
- Always verify target server.

## 🧩 Key Takeaways

- Package management is a fundamental system administration task

- Consistency across servers is critical in production environments

- Always verify installations and server context

## 📚 Reference Documentation
```bash
man yum
man zip
```


## 🤝 For Learners

If you are learning Linux:

- Always verify which server you are working on

- Install packages carefully in multi-server environments

- Think about consistency and reliability

```
⭐ If this repository helps you, consider starring it.
```