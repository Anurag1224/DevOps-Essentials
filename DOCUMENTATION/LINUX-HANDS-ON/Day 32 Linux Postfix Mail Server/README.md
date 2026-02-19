# Linux Hands-On Practice – Day 32: Postfix & Dovecot Mail Server Setup

> **Level:** Linux Level 2  
> **Focus:** Understanding mail server architecture with Postfix (MTA) and Dovecot (IMAP/POP3)

## 📌 Task Overview

| Aspect | Details |
|--------|---------|
| **Task Name** | Linux Postfix Mail Server |
| **Datacenter** | Stork DC |
| **Target Server** | Mail Server (stmail01) |

### Requirements
- [ ] Install and configure Postfix
- [ ] Create email account `ravi@stratos.xfusioncorp.com`
- [ ] Set mail directory to `/home/ravi/Maildir`
- [ ] Install and configure Dovecot

---

## 🏗️ Architecture Understanding

### 🔹 Postfix (Mail Transfer Agent)
- **Purpose:** Sends and receives emails via SMTP
- **Port:** 25
- **Function:** Handles mail routing

### 🔹 Dovecot (Mail Server)
- **Purpose:** Allows users to retrieve mail
- **Protocols:** IMAP (port 143), POP3 (port 110)
- **Connection:** Links users to Maildir storage

### 🔹 Maildir Storage
- **Location:** `/home/username/Maildir`
- **Structure:** Contains `cur/`, `new/`, `tmp/` subdirectories

---

## ⚙️ Implementation Steps

### Step 1: Install Postfix
```bash
sudo yum install -y postfix
```

### Step 2: Configure Postfix

**Edit main configuration:**
```bash
sudo vi /etc/postfix/main.cf
```

**Key configurations:**
```
myhostname = stmail01.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
home_mailbox = Maildir/
```

**Verify configuration:**
```bash
sudo postfix check
```

### Step 3: Create User Account
```bash
sudo useradd ravi
sudo passwd ravi
# Password: Rc5C9EyvbU
```

### Step 4: Create Maildir Structure
```bash
sudo mkdir -p /home/ravi/Maildir/{cur,new,tmp}
sudo chown -R ravi:ravi /home/ravi/Maildir
sudo chmod -R 700 /home/ravi/Maildir
```

### Step 5: Start & Enable Postfix
```bash
sudo systemctl start postfix
sudo systemctl enable postfix
sudo systemctl status postfix
```

### Step 6: Install Dovecot
```bash
sudo yum install -y dovecot
```

### Step 7: Configure Dovecot

**Edit main configuration:**
```bash
sudo vi /etc/dovecot/dovecot.conf
```

**Enable protocols:**
```
protocols = imap pop3
```

**Edit mail storage configuration:**
```bash
sudo vi /etc/dovecot/conf.d/10-mail.conf
```

**Set mail location:**
```
mail_location = maildir:~/Maildir
```

### Step 8: Start & Enable Dovecot
```bash
sudo systemctl start dovecot
sudo systemctl enable dovecot
sudo systemctl status dovecot
```

---

## ❌ Mistakes & Troubleshooting

### ❗ Mistake 1: Postfix Failed to Start

**Error:**
```
fatal: parameter inet_interfaces: no local interface found for ::1
```

**Root Cause:** Incorrect configuration of `inet_interfaces` and `inet_protocols`

**Solution:**
```
inet_interfaces = all
inet_protocols = all
```

Then verify and restart:
```bash
sudo postfix check
sudo systemctl restart postfix
```

---

### ❗ Mistake 2: Wrong inet_protocols Value

**Error:**
```
postfix: fatal: unknown inet_protocols value "IPv4"
```

**Root Cause:** Used invalid value `IPv4` (case-sensitive in Linux)

**Valid Values:**
- `inet_protocols = all`
- `inet_protocols = ipv4`
- `inet_protocols = ipv6`

> **Lesson:** Linux is case-sensitive; always check official documentation for correct values.

---

### ❗ Mistake 3: Dovecot Not Configured Properly

**Error Message:**
```
Mail not received!, 'dovecot' is not configured correctly
```

**Root Cause:** Maildir path mismatch or Dovecot service not enabled

**Solution:**
- Verify correct `mail_location` in configuration
- Ensure Maildir exists with proper permissions
- Enable and restart service: `sudo systemctl enable dovecot && sudo systemctl restart dovecot`

---

## 🔍 Verification Steps

**Check service status:**
```bash
systemctl status postfix
systemctl status dovecot
```

**Verify listening ports (SMTP, IMAP, POP3):**
```bash
ss -tulnp | grep -E '25|143|110'
```

**Confirm Maildir structure:**
```bash
ls -ld /home/ravi/Maildir
ls -ld /home/ravi/Maildir/{cur,new,tmp}
```

---

## 🧠 Key Concepts Learned

- ✅ Difference between MTA (Postfix) and IMAP/POP3 servers (Dovecot)
- ✅ Critical importance of correct network interface configuration
- ✅ How Linux services depend on exact config syntax and values
- ✅ Maildir structure, ownership, and permissions
- ✅ Service lifecycle management via `systemctl`
- ✅ Debugging techniques using `systemctl status` and `journalctl`

---

## 🚀 Production Thinking Reflection

This task demonstrated a **basic mail setup** only. In production environments, additional configurations are essential:

| Component | Requirement |
|-----------|-------------|
| **Security** | TLS encryption, SMTP authentication |
| **Deliverability** | DKIM, SPF, DMARC records |
| **Reliability** | Monitoring, alerting, redundancy |
| **Performance** | Spam filtering, rate limiting |
| **Operations** | Disk quotas, log rotation, backups |

### Mindset Shift
```
Before: "Install a package"
After:  "Design a mail system"
```

---

## 📚 DevOps Skills Strengthened

- 🔧 Service configuration and management
- 🐛 Debugging service failures
- ✔️ Configuration file validation
- 🌐 Understanding network listeners
- 🔐 Secure mail storage concepts
- 📋 System design thinking

---

## 🏁 Summary

**Day 32 was about much more than just installation:**

| Aspect | Learning |
|--------|----------|
| **Understanding** | Mail server architecture and component interaction |
| **Problem-Solving** | Fixing configuration errors systematically |
| **Resilience** | Learning from service failures |
| **Design** | Thinking in terms of system architecture, not just commands |

This was one of the most **concept-heavy and rewarding** tasks in the DevOps learning journey.

Linux Hands-On Practice – Day 32
Postfix & Dovecot Mail Server Setup (Linux Level 2)

This document captures Day 32 learning as part of my DevOps hands-on journey.

The focus of this task was setting up a basic mail server architecture using:

Postfix → Mail Transfer Agent (MTA)

Dovecot → IMAP/POP3 Server

Local Maildir storage

This task helped me understand how mail systems are structured and how multiple services work together to deliver and retrieve emails.

📌 Task Overview

Task Name: Linux Postfix Mail Server
Datacenter: Stork DC
Target Server: Mail Server (stmail01)

Requirements

Install and configure Postfix

Create email account ravi@stratos.xfusioncorp.com

Set mail directory to /home/ravi/Maildir

Install and configure Dovecot

🏗 Architecture Understanding

Before implementation, it's important to understand the components:

🔹 Postfix (MTA)

Sends and receives emails via SMTP

Listens on port 25

Handles mail routing

🔹 Dovecot

Allows users to retrieve mail

Provides IMAP (143) and POP3 (110)

Connects users to Maildir

🔹 Maildir

Stores emails inside:

/home/username/Maildir

⚙️ Implementation Steps
Step 1: Install Postfix
sudo yum install -y postfix

Step 2: Configure Postfix

Edit:

sudo vi /etc/postfix/main.cf


Key configurations:

myhostname = stmail01.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
home_mailbox = Maildir/


Verify configuration:

sudo postfix check

Step 3: Create User Account
sudo useradd ravi
sudo passwd ravi


Set password:

Rc5C9EyvbU

Step 4: Create Maildir Structure
sudo mkdir -p /home/ravi/Maildir/{cur,new,tmp}
sudo chown -R ravi:ravi /home/ravi/Maildir
sudo chmod -R 700 /home/ravi/Maildir

Step 5: Start & Enable Postfix
sudo systemctl start postfix
sudo systemctl enable postfix


Verify:

sudo systemctl status postfix

Step 6: Install Dovecot
sudo yum install -y dovecot

Step 7: Configure Dovecot

Edit:

sudo vi /etc/dovecot/dovecot.conf


Ensure:

protocols = imap pop3


Edit:

sudo vi /etc/dovecot/conf.d/10-mail.conf


Set:

mail_location = maildir:~/Maildir

Step 8: Start & Enable Dovecot
sudo systemctl start dovecot
sudo systemctl enable dovecot


Verify:

sudo systemctl status dovecot

❌ Mistakes & Troubleshooting

This task included several valuable troubleshooting lessons.

❗ Mistake 1: Postfix Failed to Start

Error:

fatal: parameter inet_interfaces: no local interface found for ::1


🔎 Cause:
Incorrect configuration of inet_interfaces and inet_protocols.

Fix:
Set:

inet_interfaces = all
inet_protocols = all


Then:

sudo postfix check
sudo systemctl restart postfix

❗ Mistake 2: Wrong inet_protocols Value

Error:

postfix: fatal: unknown inet_protocols value "IPv4"


🔎 Cause:
Used invalid value IPv4.

Correct values:

inet_protocols = all
inet_protocols = ipv4
inet_protocols = ipv6


Linux is case-sensitive.

❗ Mistake 3: Dovecot Not Configured Properly

Lab Failure Message:

Mail not received!, 'dovecot' is not configured correctly


🔎 Cause:
Maildir path mismatch or Dovecot not enabled.

Fix:

Set correct mail_location

Ensure Maildir exists

Restart and enable service

🔍 Verification Steps

Check services:

systemctl status postfix
systemctl status dovecot


Check listening ports:

ss -tulnp | grep -E '25|143|110'


Check Maildir exists:

ls -ld /home/ravi/Maildir

🧠 Key Concepts Learned

Difference between MTA and IMAP/POP3 server

Importance of correct network interface configuration

How Linux services depend on correct config syntax

Maildir structure and ownership

Service management via systemctl

Debugging using systemctl status and journalctl

🚀 Production Thinking Reflection

This was a basic mail setup.

In real production environments, we would additionally configure:

TLS encryption

SMTP authentication

Spam filtering

DKIM / SPF / DMARC

Firewall rules

Monitoring and alerting

Disk quota management

Log rotation

This task helped shift thinking from:
“Install a package”

To:
“Design a mail system”

📚 DevOps Skills Strengthened

Service configuration

Debugging service failures

Configuration file validation

Understanding network listeners

Secure mail storage concepts

🏁 Summary

Day 32 was not just about installing Postfix and Dovecot.

It was about:

Understanding mail server architecture

Fixing configuration errors

Learning from service failures

Thinking in terms of system design

This was one of the most concept-heavy tasks so far — and one of the most rewarding.