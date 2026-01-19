
# Linux Hands-On Practice – Day 7  
## Secure Root SSH Access (Disable Direct Root Login)

This document captures **Day 7 learning** as part of my **DevOps journey**, based on hands-on Linux security tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was **hardening SSH access** by disabling direct root login, a standard security control enforced after audits in real production environments.

---

## 📌 Task Overview

**Task Name:** Secure Root SSH Access  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Servers:** All App Servers (`stapp01`, `stapp02`, `stapp03`)

### Task Requirements
- Disable **direct SSH login for the root user**
- Apply the configuration on **all App Servers**
- Ensure non-root users can still access the servers using `sudo`

---

## 🏗 Infrastructure Context

This task reflects a **security-hardened enterprise access model**:

```
Local Access
    ↓
Jump Host (jumphost)
    ↓
App Servers (stapp01, stapp02, stapp03)
```

Direct root login is considered a security risk and is typically disabled to enforce accountability and reduce attack surface.

---

## 🧠 Key Concepts Learned

- Difference between **root access** and **direct root SSH login**
- Why direct root SSH access is a security risk
- Role of `/etc/ssh/sshd_config` in controlling SSH server behavior
- Importance of consistent security configuration across multiple servers
- Verifying SSH daemon configuration safely

---

## ⚙️ Implementation Steps

### 1. Edit SSH Server Configuration
```bash
sudo vi /etc/ssh/sshd_config
```

Locate the directive:
```
PermitRootLogin yes
```

Change it to:
```
PermitRootLogin no
```

**Important Notes:**
- Ensure the line is not commented out
- Only one active `PermitRootLogin` directive should exist
- Repeat this on all three App Servers

### 2. Restart SSH Service
```bash
sudo systemctl restart sshd
```

This step is mandatory for changes to take effect.

---

## 🔍 Verification Steps

### Verify Effective SSH Configuration
```bash
sudo sshd -T | grep permitrootlogin
```

Expected output:
```
permitrootlogin no
```

This confirms that direct root SSH login is disabled.

### Optional: Test Root Login Denial
```bash
ssh root@<server_ip>
```

Expected result:
```
Permission denied (publickey,password).
```

⚠️ **Always confirm non-root user access is working before testing this.**

---
## ❌ Common Mistakes & Learnings

**1️⃣ Editing the Wrong File**
- `sshd_config` → server-side (correct)
- `ssh_config` → client-side (incorrect)

**2️⃣ Forgetting to Restart SSH**
- Changes do not apply until `sshd` is restarted

**3️⃣ Applying the Change on Only One Server**
- Security configurations must be consistent across all nodes

---

## 🧩 Key Takeaways

- Direct root SSH login should always be disabled
- Administrative access should be performed via `sudo`
- SSH hardening is a baseline security requirement
- Verification is essential after making access changes
- Security controls must be applied consistently across servers

---

## 📚 Reference Documentation

**Linux manual pages:**
```bash
man sshd_config
man sshd
```

---

## 🤝 For Learners

- Never allow direct root SSH access in production
- Always verify SSH configuration changes
- Apply security changes uniformly across all servers
- Treat access controls as high-risk operations

Feel free to fork, reuse, or suggest improvements.
```
⭐ If this repository helps you, consider starring it.
```
