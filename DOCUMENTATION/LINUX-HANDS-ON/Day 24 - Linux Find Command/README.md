# Linux Hands-On Practice – Day 24  
## Linux Find Command (File Discovery & Safe Copy) – Linux Level 2

This document captures **Day 24 learning** as part of my **DevOps hands-on journey**, based on real-world Linux administration tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was learning how to **locate specific files and copy them safely while preserving directory structure**, which is a common requirement in security investigations and log analysis.

---

## 📌 Task Overview

**Task Name:** Linux Find Command  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** App Server 3 (`stapp03`)  
**Source Directory:** `/var/www/html/blog`  
**Destination Directory:** `/blog`

### Task Requirements

1. Find all files (not directories) with `.css` extension inside:

/var/www/html/blog


2. Copy only those files to:

/blog


3. Preserve the parent directory structure while copying.

4. Do not copy the entire directory contents.

---

## 🏗 Infrastructure Context

This task simulates a **security investigation scenario** where potentially malicious or suspicious files must be:

- Identified
- Isolated
- Copied for further analysis

Instead of deleting files immediately, teams often preserve evidence for debugging or forensic analysis.

---

## 🧠 Key Concepts Learned

- Using the `find` command to search files
- Filtering by file type and extension
- Copying selected files safely
- Preserving directory hierarchy using `cp --parents`
- Avoiding accidental bulk copy of entire directories

---

## ⚙️ Commands Used

### Step 1: Connect to App Server 3
```bash
ssh banner@stapp03
hostname
```

Verify you are on the correct server.

### Step 2: Create Destination Directory
```bash
sudo mkdir -p /blog
```

### Step 3: Locate All .css Files
```bash
sudo find /var/www/html/blog -type f -name "*.css"
```

Explanation:

- -type f → search only files

- -name "*.css" → filter by extension

### Step 4: Copy Files While Preserving Directory Structure
```bash
sudo find /var/www/html/blog -type f -name "*.css" -exec cp --parents {} /blog \;
```

Explanation:

- -exec → run command on each result

- cp --parents → preserves directory structure

## 🔍 Verification Steps

Check copied files:
```bash
ls -R /blog
```

Verify:

- Only .css files are copied

- Directory structure is preserved

- Entire source directory is not copied

🧩 Why Preserving Structure Matters

Preserving directory structure helps:

- Maintain file context

- Simplify debugging

- Avoid filename conflicts

- Support accurate forensic analysis

This is commonly used in:

- Security investigations

- Log collection

- Backup scripts

## ❌ Common Mistakes & Learnings

1️⃣ Copying Entire Directory
```bash
cp -r /var/www/html/blog /blog
```

This copies everything, which is incorrect.

2️⃣ Forgetting -type f

Directories may also get copied unintentionally.

3️⃣ Forgetting --parents

Directory structure is lost, making investigation harder.

## 🧩 Key Takeaways

- find is one of the most powerful Linux tools for file discovery

- Always test search results before performing actions

- Preserve structure when copying investigation data

- Small command options can significantly change behavior

## 📚 Reference Documentation

Linux manual pages:
```bash
man find
man cp
```

## 🤝 For Learners

If you are learning Linux:

- Always verify search results before copying or deleting

- Understand command options before running them

- Think in terms of safety and traceability

- Treat production data carefully

This task represents a real-world operational workflow used in system administration and security.

```
⭐ If this repository helps you, consider starring it.
```