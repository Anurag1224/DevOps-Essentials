# Linux Hands-On Practice – Day 20  
## Linux Banner (Login Message of the Day) – Linux Level 2

This document captures **Day 20 learning** as part of my **DevOps hands-on journey**, continuing **Linux Level 2**, based on real-world Linux compliance and security configuration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring a **standard login banner (MOTD)** across multiple servers using an approved template, ensuring consistency and compliance across the infrastructure.

This reflects how enterprises enforce legal and security policies at the system access level.

---

## 📌 Task Overview

**Task Name:** Linux Banner  
**Level:** Linux Level 2  
**Datacenter:** Stratos  

### Target Servers

- All Application Servers (`stapp01`, `stapp02`, `stapp03`)  
- All Database Servers (e.g. `stdb01`, etc.)

### Task Requirements

- Use the approved banner template located at:  
  `/home/thor/nautilus_banner` on the **Jump Host**
- Apply this banner on all App and DB servers
- The banner should be displayed **after successful login**

---

## 🏗 Infrastructure Context

In enterprise environments, login banners are required for:

- Security awareness  
- Legal compliance  
- Acceptable use policies  
- Audit requirements  

These banners typically inform users that:
- The system is monitored  
- Access is restricted to authorized users  
- Activities may be logged  

This task simulates a real compliance scenario where all servers must display a **standard, approved message** at login.

---

## 🧠 Key Concepts Learned

- What Message of the Day (MOTD) is  
- Difference between `/etc/motd` and `/etc/issue`  
- Centralized configuration using templates  
- Secure file transfer via jump hosts  
- Applying configuration changes across multiple servers  

---

## ⚙️ Commands Used

### Step 1: Login to Jump Host
```bash
ssh thor@jumphost
```

View the approved banner:
```bash
cat /home/thor/nautilus_banner
```

### Step 2: Copy Banner to Target Servers

Example for one App Server:
```bash
scp /home/thor/nautilus_banner steve@stapp02:/tmp/nautilus_banner
```

Repeat this for:

- All App Servers

- All DB Servers

### Step 3: Apply Banner on Each Server

Login to the server and run:
```bash
sudo mv /tmp/nautilus_banner /etc/motd
```

This replaces the system login banner.

## 🔍 Verification Steps

Logout and login again:
```bash
exit
ssh steve@stapp02
```

You should see the banner displayed immediately after login.

## 🔐 Why We Use a Two-Step Copy (Important)

Instead of copying directly into /etc/motd, the banner is:

1. Copied to /tmp as a normal user

2. Moved to /etc/motd using sudo

This approach is used because:

- Direct root file transfers are discouraged

- It improves auditability

- It is safer and more realistic

- It matches how automation tools work

This reflects real production practices.

## ❌ Common Mistakes & Learnings

1️⃣ Editing the Wrong File

- /etc/issue shows banner before login

- /etc/motd shows banner after login (correct one)

2️⃣ Applying Only on App Servers

- Task requires both App and DB servers

3️⃣ Forgetting Sudo

- /etc/motd requires root privileges

4️⃣ Not Verifying

- Always logout/login to confirm banner

## 🧩 Key Takeaways

- Login banners are part of security compliance

- /etc/motd controls post-login messages

- Centralized templates ensure consistency

- Jump hosts are used for controlled access

- Even small configurations matter in audits

## 📚 Reference Documentation

Linux manual pages:

```bash
man motd
man scp
```

## 🤝 For Learners

If you are learning Linux administration:

- Always understand why a configuration exists

- Follow secure file handling practices

- Apply changes consistently across environments

- Remember that compliance is part of security

Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```