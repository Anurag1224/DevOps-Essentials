# Linux Hands-On Practice – Day 29  
## Configure Sudo Access (Password-less Sudo) – Linux Level 2

This document captures **Day 29 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring **sudo access** for a user and enabling **password-less privilege escalation**, which is commonly used in automation and operational workflows.

---

## 📌 Task Overview

**Task Name:** Configure Sudo Access  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Servers:**
- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

1. Provide sudo access to user `anita` on all app servers.
2. Configure password-less sudo for this user.

---

## 🏗 Infrastructure Context

In production environments:
- Root login is often restricted
- Users perform administrative tasks using `sudo`
- Automation scripts require password-less execution

This ensures:
- Better auditing
- Controlled privilege escalation
- Improved security practices

---

## 🧠 Key Concepts Learned

- Difference between root login and sudo
- Password-less sudo configuration
- Editing sudoers safely using `visudo`
- Verifying user privileges
- Difference between authentication and authorization

---

## ⚙️ Commands Used

### Step 1: Connect to App Server
```bash
ssh tony@stapp01
hostname
```

Repeat on all app servers.

### Step 2: Open sudoers File Safely
```bash
sudo visudo
```
### Step 3: Add Entry for User anita

Add the following line:
```text
anita ALL=(ALL) NOPASSWD: ALL
```

Explanation:

Component 	| Meaning
--------------------------------------------
anita	    | Username
ALL	        | All hosts
(ALL)	    | Can run commands as any user
NOPASSWD	| No password required
ALL	        | All commands allowed
---------------------------------------------
### Step 4: Verify Sudo Access

Switch user:
```bash
sudo su - anita
```

Test:
```
sudo ls /root
```

If no password is prompted, configuration is successful.

## 🔍 Verification Steps

Check sudo privileges:

```bash
sudo -l
```

Confirm:
```
NOPASSWD: ALL
```
## 🧩 Important Concepts

Authentication vs Authorization

|Term	        | Meaning                                 |
|```````````````|`````````````````````````````````````````|
|Authentication	| Proving identity (password/SSH login)   |
|Authorization	| What actions user is allowed to perform |
``````````````````````````````````````````````````````````
Sudo handles authorization, not login authentication.

## ❌ Common Mistakes & Learnings

1️⃣ Editing sudoers file incorrectly
Always use:
```
visudo
```

2️⃣ Forgetting NOPASSWD option

User will still be prompted for password.

3️⃣ Testing using su - anita

This requires the user’s password. Use:
```bash
sudo su - anita
```
## 🧩 Key Takeaways

- Sudo provides controlled administrative access

- Password-less sudo is useful for automation

- Always verify privilege configuration

- Authentication and authorization are separate concepts

## 📚 Reference Documentation
```bash
man sudo
man visudo
```

## 🤝 For Learners

If you are learning Linux:

- Never edit /etc/sudoers directly

- Always test privilege changes

- Understand the difference between login and privilege escalation

```
⭐ If this repository helps you, consider starring it.
```