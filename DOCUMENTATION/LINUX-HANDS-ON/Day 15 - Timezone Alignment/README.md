# Linux Hands-On Practice – Day 15  
## Timezone Alignment (Linux Level 1)

This document captures **Day 15 learning** as part of my **DevOps hands-on journey**, based on real-world Linux system time configuration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was synchronizing the **system timezone across multiple servers** to ensure consistency with the local datacenter timezone.

This reflects how time configuration is managed in real production environments to maintain accurate logs, scheduling, and monitoring.

---

## 📌 Task Overview

**Task Name:** Timezone Alignment  
**Level:** Linux Level 1  
**Datacenter:** Stratos  

### Target Servers (All App Servers)

- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

- Identify the current timezone on each App Server  
- Update the timezone to match the datacenter standard  
- Set timezone to: `America/Belize`  
- Ensure consistency across all App Servers  

---

## 🏗 Infrastructure Context

In distributed systems, servers often generate:

- Logs  
- Alerts  
- Reports  
- Backup schedules  
- Cron jobs  

All of these rely on **system time**.

If servers operate in different timezones:
- Log correlation becomes difficult  
- Debugging incidents becomes confusing  
- Scheduled tasks may run at incorrect times  
- Audits and compliance checks can fail  

This task simulates a real operational scenario where all systems must follow a **standard timezone policy**.

---

## 🧠 Key Concepts Learned

- Understanding how Linux manages system time  
- Difference between system time and timezone  
- Importance of consistent time across servers  
- Using `timedatectl` for time configuration  
- Verifying changes without rebooting systems  

---

## ⚙️ Commands Used

### Step 1: Check Current Timezone
Run on **each App Server**:

```bash
timedatectl
```

Look for:

Time zone: ...


This shows the current configured timezone.

### Step 2: Set Timezone to America/Belize
```bash
sudo timedatectl set-timezone America/Belize
```

This updates the system timezone immediately.

### Step 3: Verify Configuration
```bash
timedatectl
```

Expected output:
```
Time zone: America/Belize
```
## 🔍 Important Notes

- No reboot is required

- Timezone changes apply instantly

- Command must be executed on all App Servers

- System clock remains the same; only the timezone changes

## ❌ Common Mistakes & Learnings

1️⃣ Updating Only One Server

- All App Servers must follow the same timezone

2️⃣ Using date Instead of timedatectl

- date only displays time, it does not configure it

3️⃣ Forgetting to Verify

- Always confirm with timedatectl

4️⃣ Rebooting the System

- Not required and unnecessary

## 🧩 Key Takeaways

- Time consistency is critical in distributed systems

- Timezone affects logs, cron jobs, and monitoring

- timedatectl is the standard tool for time management

- Configuration changes should be validated immediately

- Operational accuracy depends on aligned system time

## 📚 Reference Documentation

Linux manual pages:
```bash
man timedatectl
```

## 🤝 For Learners

- If you are learning Linux system administration:

- Treat time configuration as a critical system setting

- Always align time across distributed systems

- Validate changes before moving on

- Remember that small misconfigurations can cause big issues

Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```