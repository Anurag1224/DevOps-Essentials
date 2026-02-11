# Linux Hands-On Practice – Day 27  
## Configure Local Yum Repository – Linux Level 2

This document captures **Day 27 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was configuring a **local YUM repository** and installing packages from it. This is a common practice in enterprise environments where servers may not have internet access or where package versions must be controlled internally.

---

## 📌 Task Overview

**Task Name:** Configure Local Yum Repository  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** Backup Server (`stbkp01`)  

### Task Requirements

1. Use RPM packages located at:
    /packages/downloaded_rpms/

2. Create a local YUM repository:
- Repository ID: `epel_local`
- Base URL: `/packages/downloaded_rpms/`

3. Install the package:
    samaba

using this repository.

---

## 🏗 Infrastructure Context

In production environments, organizations often use **local repositories** because:

- Servers may not have internet access
- Security policies restrict external downloads
- Faster installations within internal networks
- Better control over package versions

This approach is common in:
- Banking systems
- Government infrastructure
- Private data centers
- Air-gapped environments

---

## 🧠 Key Concepts Learned

- What a YUM repository is
- Difference between remote and local repositories
- Repository configuration files
- Installing packages from a local source
- Refreshing YUM cache and verifying repositories

---

## ⚙️ Commands Used

### Step 1: Connect to Backup Server
```bash
ssh clint@stbkp01
hostname
```
### Step 2: Verify Package Directory

```bash
ls /packages/downloaded_rpms/
```

Confirm .rpm packages exist.

### Step 3: Create Repository File
```bash
sudo vi /etc/yum.repos.d/epel_local.repo
```

Add:
```
[epel_local]
name=epel_local
baseurl=file:///packages/downloaded_rpms
enabled=1
gpgcheck=0
```
### Step 4: Refresh Yum Cache
```bash
sudo yum clean all
sudo yum repolist
```

Verify that epel_local appears.

### Step 5: Install Samba Package
```bash
sudo yum install samba -y
```

## 🔍 Verification Steps

Check installation:
```bash
rpm -qa | grep samba
```

Confirm:

- Package installed successfully

- Repository is recognized by yum

## 🧩 Why Local Repositories Matter

Local repositories help in:

- Faster installations inside networks

- Preventing unauthorized downloads

- Maintaining approved package versions

- Supporting offline environments

They are a key part of enterprise infrastructure management.

## ❌ Common Mistakes & Learnings

1️⃣ Incorrect base URL format
Use:
```
file:///path
```

Not:
```
file://path
```

2️⃣ Forgetting to refresh yum cache
- Repositories may not appear until cache is rebuilt.

3️⃣ Incorrect repository file name or syntax
- Yum ignores invalid repo files.

## 🧩 Key Takeaways

- A repository is simply a storage location for packages

- Yum installs software from configured repositories

- Local repositories improve control, security, and reliability

- Understanding package management is essential for DevOps roles

## 📚 Reference Documentation
```bash
man yum
man yum.conf
```

## 🤝 For Learners

If you are learning Linux:

- Understand how package managers work internally

- Practice configuring repositories manually

- Always verify installations and repositories

```
⭐ If this repository helps you, consider starring it.
```