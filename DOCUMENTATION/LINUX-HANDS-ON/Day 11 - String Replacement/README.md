# Linux Hands-On Practice – Day 11  
## String Replacement using sed (Linux Level 1)

This document captures **Day 11 learning** as part of my **DevOps hands-on journey**, based on real-world Linux text manipulation tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was performing **in-place string replacement** inside a configuration file using standard Linux text processing tools.

This mirrors how configuration values are updated automatically in real production environments.

---

## 📌 Task Overview

**Task Name:** String Replacement  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** Backup Server  
**Target File:** `/root/nautilus.xml`

### Task Requirements

- Locate the file `/root/nautilus.xml`
- Replace **all occurrences** of the string `About`
- With the new string `Maritime`
- Save the changes to the same file

---

## 🏗 Infrastructure Context

The backup server stores XML templates used by the Nautilus application.

Before these templates are used, they must be populated with valid data.  
This task simulates a **routine maintenance operation** where static values in configuration files are updated programmatically.

---

## 🧠 Key Concepts Learned

- Difference between **viewing** and **modifying** files
- Using `sed` for non-interactive text replacement
- Importance of global replacement (`g` flag)
- In-place file editing using `-i`
- Verifying changes using `grep`

---

## ⚙️ Commands Used

### Step 1: Replace String in File
```bash
sudo sed -i 's/About/Maritime/g' /root/nautilus.xml
```
This command:

- Finds all occurrences of About

- Replaces them with Maritime

- Saves changes directly to the file