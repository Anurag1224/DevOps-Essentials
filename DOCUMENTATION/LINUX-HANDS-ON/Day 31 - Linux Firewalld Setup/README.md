# Linux Hands-On Practice – Day 31  
## Linux Firewalld Setup (Linux Level 2)

This document captures **Day 31 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring a firewall using **firewalld** to control access to services running on different ports. This reflects how production environments expose only necessary services to external networks.

---

## 📌 Task Overview

**Task Name:** Linux Firewalld Setup  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Servers:**
- App Server 1 (`stapp01`)
- App Server 2 (`stapp02`)
- App Server 3 (`stapp03`)

### Task Requirements

1. Install and configure **firewalld** on all app servers.
2. Allow all incoming connections on **port 80 (Nginx)**.
3. Block all incoming connections on **port 8080 (Apache)**.
4. All rules must be **permanent**.
5. Firewall zone should be **public**.
6. Ensure **Apache and Nginx services are running**.

---

## 🏗 Infrastructure Context

Typical production architecture:

Client → Nginx (port 80) → Apache (port 8080)

Nginx:
- Public-facing reverse proxy
- Handles incoming traffic

Apache:
- Backend service
- Should not be directly exposed

Firewalls enforce this separation by allowing only required ports.

---

## 🧠 Key Concepts Learned

- Purpose of firewalld
- Difference between runtime and permanent rules
- Firewall zones and their role
- Controlling port access
- Verifying firewall rules
- Relationship between services and network exposure

---

## ⚙️ Commands Used

### Step 1: Connect to Server
```bash
ssh tony@stapp01
hostname
```

Repeat on all app servers.

### Step 2: Install Firewalld
```bash
sudo yum install -y firewalld
```

### Step 3: Start and Enable Firewalld
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

Verify:
```bash
systemctl status firewalld
```

### Step 4: Check Default Zone
```bash
firewall-cmd --get-default-zone
```

If not public:
```bash
sudo firewall-cmd --set-default-zone=public
```

### Step 5: Allow Port 80 Permanently
```bash
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
```

### Step 6: Block Port 8080

If already allowed:
```bash
sudo firewall-cmd --permanent --zone=public --remove-port=8080/tcp
```

### Step 7: Reload Firewall
```bash
sudo firewall-cmd --reload
```

Permanent rules apply only after reload.

### Step 8: Ensure Services Are Running

Start Apache:
```bash
sudo systemctl start httpd
```

Start Nginx:
```bash
sudo systemctl start nginx
```

Verify:
```bash
systemctl status httpd
systemctl status nginx
```

### Step 9: Verify Firewall Rules
```bash
firewall-cmd --list-ports
```

Expected output:
```
80/tcp
```
Port 8080 should not appear.

## 🔍 Verification Steps

Check firewall status:
```bash
firewall-cmd --state
```

Check allowed ports:
```bash
firewall-cmd --list-ports
```

Check zone configuration:
```bash
firewall-cmd --get-default-zone
```
## 🧩 How Firewalld Works Internally

Firewalld manages firewall rules dynamically and communicates with the Linux kernel’s networking stack.

Traffic flow:

Internet → Firewall → Service

Rules determine:

- Which ports are reachable

- Which services remain protected

Firewalld typically uses nftables internally as its rule engine.

## ❌ Common Mistakes & Learnings

1️⃣ Forgetting the --permanent flag
Rules disappear after reboot.

2️⃣ Forgetting to reload firewall
Permanent rules are not applied immediately.

3️⃣ Opening wrong ports
Always verify service ports before allowing traffic.

4️⃣ Not verifying services are running
Firewall rules alone do not start services.

## 🧩 Key Takeaways

- Firewalls control network exposure

- Only necessary ports should be open

- Runtime and permanent configurations differ

- Verification is essential after firewall changes

- Reverse proxy architectures are common in production

## 📚 Reference Documentation
```bash
man firewall-cmd
man firewalld
```

## 🤝 For Learners

If you are learning Linux administration:

- Always verify open ports

- Understand service architecture before configuring firewalls

- Think in terms of minimizing exposure

```
⭐ If this repository helps you, consider starring it.
```