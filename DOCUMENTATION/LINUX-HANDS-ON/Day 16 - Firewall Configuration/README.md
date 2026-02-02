# Linux Hands-On Practice – Day 16  
## Firewall Configuration (Linux Level 1)

This document captures **Day 16 learning** as part of my **DevOps hands-on journey**, based on real-world Linux network security tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring the system firewall to allow access to a newly deployed web application, while maintaining proper security boundaries using firewall zones.

This reflects how services are exposed in production environments through controlled firewall rules.

---

## 📌 Task Overview

**Task Name:** Firewall Configuration  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** Backup Server (`stbkp01`)  

### Task Requirements

- Allow all incoming connections on port `8082/tcp`  
- Ensure the active firewall zone is set to `public`  
- Apply changes permanently  
- Do not open unnecessary ports  

---

## 🏗 Infrastructure Context

In real-world infrastructures, even if a service is running correctly, it remains inaccessible unless the firewall explicitly allows traffic to its port.

Firewalls act as the **first layer of defense**, controlling which network requests are permitted to reach system services.

This task simulates a common operational scenario where a new web-based tool is deployed and must be securely exposed to users.

---

## 🧠 Key Concepts Learned

- Understanding the role of `firewalld` in Linux  
- Concept of firewall zones and trust levels  
- Difference between temporary and permanent rules  
- Importance of opening only required ports  
- Verifying firewall configuration after changes  

---

## ⚙️ Commands Used

### Step 1: Login to Backup Server
```bash
ssh clint@stbkp01
hostname
```
Expected output:
```
stbkp01
```

### Step 2: Check Active Firewall Zone
```bash
firewall-cmd --get-active-zones
```

Expected output:
```
public
```

If not:
```bash
sudo firewall-cmd --set-default-zone=public
```

### Step 3: Allow Port 8082/tcp
```bash
sudo firewall-cmd --zone=public --add-port=8082/tcp --permanent
```

This allows incoming TCP connections on port 8082 permanently.

### Step 4: Reload Firewall Rules
```bash
sudo firewall-cmd --reload
```

Applies the new configuration.

### Step 5: Verify Configuration
```bash
sudo firewall-cmd --zone=public --list-ports
```

Expected output:
```
8082/tcp
```
🔍 Important Notes

- The rule is applied permanently using --permanent

- Reloading is required for changes to take effect

- Only the required port is opened

- No reboot is necessary

## ❌ Common Mistakes & Learnings

1️⃣ Opening Ports on the Wrong Server

- Firewall rules must be applied on the server hosting the service

2️⃣ Forgetting the --permanent Flag

- Rules without it are lost after reboot

3️⃣ Forgetting to Reload Firewall

- Changes won’t apply until reloaded

4️⃣ Opening Too Many Ports

- Increases attack surface unnecessarily

## 🧩 Key Takeaways

- Firewalls block traffic by default

- Services must be explicitly exposed

- Zones define trust levels

- Security is about allowing only what is needed

- Networking issues often look like application failures

## 📚 Reference Documentation

Linux manual pages:
```bash
man firewall-cmd
```

🤝 For Learners

If you are learning Linux networking:

- Always confirm the target server

- Understand firewall zones before changing rules

- Open only required ports

- Verify configuration after changes

- Treat firewalls as a critical security control

Feel free to fork, reuse, or suggest improvements.


```
⭐ If this repository helps you, consider starring it.
```