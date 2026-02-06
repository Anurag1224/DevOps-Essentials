# Linux Hands-On Practice – Day 23  
## Linux SSH Authentication (Password-less SSH) – Linux Level 2

This document captures **Day 23 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was understanding how to configure **password-less SSH authentication**, which is a fundamental requirement for automation tools, remote administration, and large-scale infrastructure management.

---

## 📌 Task Overview

**Task Name:** Linux SSH Authentication  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Source Server:** Jump Host (`jumphost`)  
**Target Servers:**  
- App Server 1 (`stapp01`)  
- App Server 2 (`stapp02`)  
- App Server 3 (`stapp03`)  

### Task Requirements

Configure **password-less SSH authentication** from:

User `thor` on Jump Host  
→ to all App Servers  
→ using their respective sudo users:
- `tony` (App Server 1)
- `steve` (App Server 2)
- `banner` (App Server 3)

---

## 🏗 Infrastructure Context

In real production environments, scripts and automation tools frequently need to run commands across multiple servers.

Examples include:
- Configuration management (Ansible)
- Backup automation
- Monitoring and maintenance jobs
- CI/CD deployments

Password-based authentication is not practical for such workflows, so **SSH key-based authentication** is used.

---

## 🧠 Key Concepts Learned

- Difference between password authentication and key-based authentication
- How SSH uses **public/private key pairs**
- Role of the `.ssh` directory
- Importance of correct permissions
- How authentication happens using cryptographic signatures
- Why password-less SSH is widely used in automation

---

## ⚙️ Commands Used

### Step 1: Login to Jump Host
```bash
ssh thor@jumphost
hostname
```

Verify you are on the jump host before proceeding.

### Step 2: Generate SSH Key (if not present)
```bash
ssh-keygen
```

Press Enter to accept defaults.

This creates:
```
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```

### Step 3: Copy Public Key to App Servers
```bash
ssh-copy-id tony@stapp01
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```

This adds the public key to:
```
~/.ssh/authorized_keys
```

on each server.

### Step 4: Verify Password-less Login
```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

Successful login without password confirms correct setup.

## 🔍 Verification Steps

Check key files:
```bash
ls -l ~/.ssh
```

Check remote authorized keys:
```bash
cat ~/.ssh/authorized_keys
```

Test SSH login without password.

## 🧩 How SSH Key Authentication Works

- Server sends a challenge

- Client signs it using the private key

- Server verifies using the public key

- Access is granted

- The private key never leaves the client machine, making this method secure.

## ❌ Common Mistakes & Learnings
1️⃣ Generating Keys on the Wrong Machine

- Keys must be generated on the client (jump host).

2️⃣ Copying Keys as the Wrong User

- Authentication is user-specific.

3️⃣ Incorrect File Permissions

- SSH requires strict permissions on .ssh and key files.

## 🧩 Key Takeaways

- SSH key authentication enables secure automation

- Password-less login is safer and more scalable than passwords

- Public keys are shared, private keys must remain secret

- SSH is a foundational technology used by most DevOps tools

## 📚 Reference Documentation

Linux manual pages:
```bash
man ssh
man ssh-copy-id
man ssh-keygen
```

## 🤝 For Learners

If you are learning Linux:

- Understand how authentication works, not just commands

- Always protect private keys

- Verify connections after configuration

- Think about scalability and automation

- Password-less SSH is a core building block in modern infrastructure and DevOps workflows.
```
⭐ If this repository helps you, consider starring it.
```