
# Linux Hands-On Practice – Day 6  
## File Ownership Filtering and Structured Data Relocation (Linux Level 1)

This document captures **Day 6 learning** as part of my **DevOps journey**, based on hands-on Linux tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was identifying files based on **user ownership**, excluding directories, and copying the data while **preserving the original directory structure**—a common requirement during production cleanup and incident resolution.

---

## 📌 Task Overview

**Task Name:** File Ownership Filtering and Data Relocation  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 3 (`stapp03`)

### Task Requirements
- Locate all **files (not directories)** owned by user `james`
- Search within `/home/usersdata`
- Copy the matched files to `/news`
- Preserve the original directory structure during copy
- Perform the task on **App Server 3**

---

## 🏗 Infrastructure Context

This task simulates a **production data cleanup scenario**:

Local Access  
↓  
Jump Host (jumphost)  
↓  
App Server 3 (`stapp03`)

Accidental data mixing in shared directories is common in real systems. Ownership-based filtering is often the safest way to isolate user-specific data.

---

## 🧠 Key Concepts Learned

- Difference between **files and directories** in Linux
- Filtering data using **file ownership**
- Safe use of `find` for targeted operations
- Preserving directory hierarchy during copy operations
- Avoiding destructive or overly broad filesystem commands

---

## ⚙️ Commands Used

### Ensure Destination Directory Exists
```bash
sudo mkdir -p /news
```

### Finding Files by Owner
Use `find` command to locate files owned by a specific user:
```bash
find /home/usersdata -type f -user james
```
- `-type f`: Matches files only (excludes directories)
- `-user james`: Filters by owner

### Copying Files with Structure Preservation
Use `cp` with `--parents` flag:
```bash
find /home/usersdata -type f -user james -exec cp --parents {} /news \;
```

### Verifying the Copy
```bash
ls -R /news
```

## Key Takeaways
- Use `-type f` to exclude directories
- `-user` flag filters by file owner
- `--parents` maintains full directory paths during copy

### What This Task Teaches

**1. File System Fundamentals**
- Understanding the distinction between files and directories is foundational to Linux administration
- Ownership is a core security concept; every file/directory has an owner and group

**2. Problem-Solving with `find`**
- The `find` command is one of the most powerful tools in Linux—mastering its predicates (`-type`, `-user`, `-name`, etc.) opens possibilities
- Combining predicates allows you to write precise queries instead of manual browsing

**3. Safe Data Operations**
- In production, copying data is not trivial—you must preserve structure and ownership to avoid breaking applications
- The `--parents` flag demonstrates how tools can solve real architectural challenges

**4. Why This Matters in DevOps**
- Automation relies on identifying resources correctly before acting on them
- A misconfigured command affecting thousands of files can be catastrophic
- These skills transfer to container orchestration, infrastructure provisioning, and log analysis

### Common Mistakes to Avoid
- Forgetting `-type f` results in copying directories unnecessarily
- Not using `--parents` flattens the directory structure, breaking application paths
- Running without verification (dry-run first) on unfamiliar systems


