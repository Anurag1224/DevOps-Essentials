# Linux Hands-On Practice – Day 25  
## Installing Ansible (Automation Setup) – Linux Level 2

This document captures **Day 25 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was preparing a **Jump Host as an Ansible controller**, which is commonly used in infrastructure automation and configuration management.

---

## 📌 Task Overview

**Task Name:** Install Ansible  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** Jump Host (`jumphost`)  

### Task Requirements

1. Install **Ansible version 4.10.0**
2. Use **pip3 only** for installation
3. Ensure Ansible command is available globally (all users can run it)

---

## 🏗 Infrastructure Context

In real-world environments:

- A **Jump Host** often acts as an **Ansible Controller**
- Automation tools execute tasks on multiple servers remotely
- SSH is used to manage systems without installing agents

This setup helps:
- Reduce manual work
- Maintain consistency across servers
- Enable repeatable deployments

---

## 🧠 Key Concepts Learned

- What an Ansible controller is
- Installing software using `pip3`
- Managing specific software versions
- Difference between user-level and system-wide installations
- Importance of version control in automation tools

---

## ⚙️ Commands Used

### Step 1: Connect to Jump Host
```bash
ssh thor@jumphost
hostname
```

Verify you are on the correct server.

### Step 2: Verify Python3 and pip3
```bash
python3 --version
pip3 --version
```

If pip3 is missing:
```bash
sudo yum install python3-pip -y
```

### Step 3: Install Ansible Version 4.10.0
```bash
sudo pip3 install ansible==4.10.0
```

Explanation:

- pip3 installs Python packages

- ==4.10.0 ensures exact version
- sudo installs system-wide


### Step 4: Verify Installation
```bash
ansible --version
```

Expected output should display:
```
ansible 4.10.0
```
## 🔍 Verification Steps

Check:
```bash
which ansible
```

This confirms the binary is available globally.

Optional test:
```bash
ansible --version
```

## 🧩 Why pip3 Instead of yum?

Reasons:

- Precise version control

- Faster updates

- Common practice in automation environments

- Required in many enterprise workflows

## ❌ Common Mistakes & Learnings

1️⃣ Installing without sudo
- Result: Ansible works only for one user

2️⃣ Installing wrong version
- Always specify version explicitly

3️⃣ Installing via yum instead of pip3
- May install incorrect version

## 🧩 Key Takeaways

- Ansible controllers manage multiple systems from a central location

- Version control is important in automation tools

- pip3 provides flexibility and precision in installations

- Automation begins with properly preparing the control node

## 📚 Reference Documentation
```bash
man pip3
ansible --help
```

## 🤝 For Learners

If you are learning Linux and DevOps:

- Understand why tools are installed, not just how

- Learn version control and dependency management

- Automation starts with mastering the basics

```
⭐ If this repository helps you, consider starring it.
```