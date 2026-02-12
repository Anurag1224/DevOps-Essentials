# Linux Hands-On Practice – Day 28  
## Linux Services (Install and Enable nscd) – Linux Level 2

This document captures **Day 28 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was understanding how to **install, start, and enable system services**, which is essential for maintaining application dependencies and ensuring services run reliably after system reboots.

---

## 📌 Task Overview

**Task Name:** Linux Services  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Servers:**
- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

1. Install the **nscd** package on all application servers.  
2. Ensure the service is **enabled to start at boot**.

---

## 🏗 Infrastructure Context

Many applications depend on background services.  
If a required service is not running or fails to start after a reboot, applications may fail or behave unpredictably.

Ensuring services are:
- Installed
- Running
- Enabled at boot

is a critical operational responsibility in system administration.

---

## 🧠 Key Concepts Learned

- Difference between installing a package and running a service
- Managing services using `systemctl`
- Difference between `start` and `enable`
- Verifying service status
- Importance of enabling services for reliability

---

## ⚙️ Commands Used

### Step 1: Connect to Application Server
```bash
ssh tony@stapp01
hostname
```

Repeat on all app servers.

### Step 2: Install nscd Package

```bash
sudo yum install -y nscd
```

Verify installation:

```bash
rpm -qa | grep nscd
```

## Step 3: Start the Service
```bash
sudo systemctl start nscd
```

## Step 4: Enable Service at Boot
```bash
sudo systemctl enable nscd
```

### Step 5: Verify Service Status
```bash
systemctl status nscd
```

Confirm:
```
Active (running)
Enabled
```

## 🔍 Verification Steps

Check service status:
```bash
systemctl status nscd
```

Check if enabled:
```bash
systemctl is-enabled nscd
```

## 🧩 Important Concept: Start vs Enable

Command	    Purpose
start	    Runs service immediately
enable	    Starts service automatically at boot


Think:
 Start = Present
 Enable = Future

## ❌ Mistakes Made & Learnings

While performing the task, I initially started the service but forgot to enable it at boot.

This reinforced an important lesson:

- A running service does not guarantee it will start after reboot.

- Always verify both running status and enabled state.

- This is a common operational oversight in real environments.

## 🧩 Key Takeaways

- Installing a package does not mean the service is running

- Services must be enabled to survive reboots

- systemctl is a core tool for managing services

- Small configuration steps can prevent real production issues

## 📚 Reference Documentation

```bash
man systemctl
man nscd
```


## 🤝 For Learners

If you are learning Linux:

- Always verify services after installation

- Remember to enable critical services

-Understand the difference between runtime state and boot configuration

```
⭐ If this repository helps you, consider starring it.
```