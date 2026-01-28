# Linux Hands-On Practice – Day 14  
## Default GUI Boot Configuration (Linux Level 1)

This document captures **Day 14 learning** as part of my **DevOps hands-on journey**, based on real-world Linux system boot configuration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring the **default boot target** of Linux systems to enable **GUI mode**, while ensuring no service disruption by avoiding an immediate reboot.

This closely mirrors how configuration changes are handled in real production environments.

---

## 📌 Task Overview

**Task Name:** Default GUI Boot Configuration  
**Level:** Linux Level 1  
**Datacenter:** Stratos  

### Target Servers (All App Servers)

- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

- Configure all App Servers to boot into **GUI mode by default**
- Use the appropriate systemd target
- **Do not reboot** any server after making the change

---

## 🏗 Infrastructure Context

Linux systems boot into different operational modes depending on how they are configured.

In modern Linux distributions using **systemd**, this behavior is controlled using **targets**.

In production environments:
- Servers usually boot into non-GUI mode to conserve resources
- GUI mode is enabled only when required by specific tools or workflows
- Configuration changes are applied cautiously without immediate reboots

This task simulates a real operational scenario where systems are **prepared for future behavior changes** without causing downtime.

---

## 🧠 Key Concepts Learned

- Difference between **text mode** and **GUI mode**
- Understanding systemd targets vs legacy runlevels
- How Linux determines its default boot behavior
- Importance of validating system state before applying changes
- Applying configuration changes safely across multiple servers

---

## ⚙️ Commands Used

### Step 1: Verify Current Default Target
Run on **each App Server**:

```bash
systemctl get-default
```
Typical output before change:
```
multi-user.target
```

Or, in some cases:
```
graphical.target
```
### Step 2: Set GUI as Default Boot Target

Run only if the target is not already set:
```bash
sudo systemctl set-default graphical.target
```
```
This updates the system configuration to boot into GUI mode by default on the next reboot.
```
### Step 3: Verify Configuration
```bash
systemctl get-default
```

Expected output:
```
graphical.target
```

## 🔍 Important Notes

- No reboot is performed as part of this task

- Changes will take effect only on the next system reboot

- If a server already had graphical.target set, no action was required

- This follows the principle of idempotence (do not change what is already correct)

## ❌ Common Mistakes & Learnings

1️⃣ Rebooting the Server

- Reboots are disruptive and often require approval in real environments

2️⃣ Using Legacy Runlevel Commands

- Modern systems use systemd targets, not init runlevels

3️⃣ Applying Changes Without Verification

- Always check current system state before modifying it

4️⃣ Configuring Only One Server

- Task explicitly requires changes on all App Servers

## 🧩 Key Takeaways

- Linux boot behavior is configurable and controlled via systemd targets

- GUI mode should be enabled only when required

- Production changes should avoid unnecessary downtime

- Verifying system state is as important as making changes

- Configuration consistency across servers is critical

## 📚 Reference Documentation

Linux manual pages:
```
man systemctl
```

## 🤝 For Learners

If you are learning Linux system administration:

- Always understand why a configuration exists

- Validate system state before applying changes

- Avoid reboots unless explicitly required

- Think in terms of production impact, not just task completion

Feel free to fork, reuse, or suggest improvements.

```
⭐ If this repository helps you, consider starring it.
```