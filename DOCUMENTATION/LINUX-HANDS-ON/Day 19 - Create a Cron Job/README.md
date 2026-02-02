# Linux Hands-On Practice – Day 19  
## Create a Cron Job (Linux Level 2)

This document captures **Day 19 learning** as part of my **DevOps hands-on journey**, marking the start of **Linux Level 2**, based on real-world Linux automation tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was setting up and validating a **cron job across multiple servers**, ensuring that the required services are installed, running, and configured correctly.

This reflects how automation is tested and rolled out in production environments before deploying real operational scripts.

---

## 📌 Task Overview

**Task Name:** Create a Cron Job  
**Level:** Linux Level 2  
**Datacenter:** Stratos  

### Target Servers (All App Servers)

- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

a. Install the `cronie` package and start the `crond` service  
b. Add the following cron job for the **root user**:

```bash
*/5 * * * * echo hello > /tmp/cron_text
```
This job should run every 5 minutes.

## 🏗 Infrastructure Context

In Linux systems, scheduled automation is handled by the cron service.

Cron is widely used for:

- Backups

- Log rotation

- Cleanup jobs

- Health checks

- Monitoring tasks

However, cron jobs only work if:

- The cron service is installed

- The service is running

- The job is added for the correct user

This task simulates how system administrators test automation before deploying real scripts in production.

## 🧠 Key Concepts Learned

Difference between cron configuration and cron service

- Importance of installing required packages

- Managing system services with systemctl

- Creating cron jobs for specific users

- Verifying scheduled automation

## ⚙️ Commands Used

### Step 1: Login to Each App Server
```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

Verify:
```bash
hostname
```
### Step 2: Install Cron Service
```bash
sudo yum install -y cronie
```

This installs the cron scheduler.

### Step 3: Start and Enable Cron
```bash
sudo systemctl start crond
sudo systemctl enable crond
```

Verify:
```bash
systemctl status crond
```

Expected:
```
active (running)
```
### Step 4: Switch to Root User
```bash
sudo su -
```

### Step 5: Add Cron Job
```bash
crontab -e
```

Add:
```bash
*/5 * * * * echo hello > /tmp/cron_text
```

Save and exit.

## 🔍 Verification Steps

Wait 5 minutes, then:
```bash
cat /tmp/cron_text
```

Expected output:
```
hello
```

This confirms the cron job is executing successfully.

## ❌ Common Mistakes & Learnings

1️⃣ Cron Service Not Installed

- Cron jobs won’t run without cronie

2️⃣ Cron Service Not Running

- Service must be active (crond)

3️⃣ Adding Cron for Wrong User

- Task requires cron job for root

4️⃣ Not Waiting for Execution

- Job runs every 5 minutes, not instantly

5️⃣ Testing on Only One Server

- Must be applied on all App Servers

## 🧩 Key Takeaways

- Cron automation depends on running services

- Automation always runs in a user context

- Verification is mandatory for scheduled tasks

- Real automation involves multiple system layers

- Testing small jobs is critical before production rollout

## 📚 Reference Documentation

Linux manual pages:
```bash
man cron
man crontab
man systemctl
```

## 🤝 For Learners

- If you are learning Linux automation:

- Always ensure services are installed and running

- Understand which user executes automated jobs

- Start with simple test commands

- Verify outputs before moving to complex scripts

Feel free to fork, reuse, or suggest improvements.


```
⭐ If this repository helps you, consider starring it.
```