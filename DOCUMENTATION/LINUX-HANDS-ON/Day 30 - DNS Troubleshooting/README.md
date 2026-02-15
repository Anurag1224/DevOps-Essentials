# Linux Hands-On Practice – Day 30  
## DNS Troubleshooting (Linux Level 2)

This document captures **Day 30 learning** as part of my **DevOps hands-on journey**, based on real-world Linux troubleshooting tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was diagnosing and resolving **DNS resolution issues** by configuring additional nameservers.

---

## 📌 Task Overview

**Task Name:** DNS Troubleshooting  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** App Server 2 (`stapp02`)

### Task Requirements

- Identify DNS resolution issues
- Add Google Public DNS servers as a temporary fix

---

## 🏗 Infrastructure Context

DNS (Domain Name System) is responsible for converting domain names into IP addresses.

If DNS fails:
- Websites cannot be reached
- Package installations fail
- External services become unreachable

Because of this, DNS troubleshooting is one of the most common operational tasks in production environments.

---

## 🧠 Key Concepts Learned

- Role of DNS in Linux networking
- Purpose of `/etc/resolv.conf`
- Temporary DNS configuration methods
- Testing DNS resolution
- Importance of troubleshooting fundamentals

---

## ⚙️ Commands Used

### Step 1: Connect to Server
```bash
ssh steve@stapp02
hostname
```

### Step 2: Check Current DNS Configuration

```bash
cat /etc/resolv.conf
```

### Step 3: Edit DNS Configuration

```bash
sudo vi /etc/resolv.conf
```

Add:
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

### Step 4: Verify DNS Resolution
```
ping google.com
```

or
```
nslookup google.com
```
## 🔍 Verification Steps

Confirm DNS servers:
```bash
cat /etc/resolv.conf
```

Test resolution:
```
ping google.com
```

## ❌ Common Mistakes & Learnings

1️⃣ Editing wrong configuration file

DNS servers must be configured in /etc/resolv.conf.

2️⃣ Incorrect syntax

Correct format:
```
nameserver 8.8.8.8
```

3️⃣ Forgetting to verify connectivity

Always test resolution after making changes.

## 🧩 Key Takeaways

- DNS is critical for connectivity and application functionality

- Troubleshooting often begins with verifying basic components

- /etc/resolv.conf controls name resolution in Linux

- Temporary fixes are sometimes necessary to restore services quickly

## 📚 Reference Documentation

```bash
man resolv.conf
man nslookup
```

## 🤝 For Learners

If you are learning Linux troubleshooting:

- Always verify DNS when connectivity issues arise

- Understand configuration files before modifying them

- Test after every change

```
⭐ If this repository helps you, consider starring it.
```