# Linux Hands-On Practice – Day 22  
## Linux String Substitute using sed (Linux Level 2)

This document captures **Day 22 learning** as part of my **DevOps hands-on journey**, based on real-world Linux text processing tasks from the **KodeKloud Engineer – Nautilus Project**.

The focus of this task was understanding how Linux tools like `grep` and `sed` are used to **safely manipulate data inside files**, which is a common requirement in log processing, configuration management, and automation workflows.

---

## 📌 Task Overview

**Task Name:** Linux String Substitute (sed)  
**Level:** Linux Level 2  
**Datacenter:** Stratos  
**Target Server:** App Server 2 (`stapp02`)  
**Target File:** `/home/BSD.txt`

### Task Requirements

1. Delete all lines containing the word **code** (case-sensitive)  
   Save output to: `/home/BSD_DELETE.txt`

2. Replace all occurrences of the exact word **and** with **their**  
   (Do not replace partial matches like *android, candy, standard*)  
   Save output to: `/home/BSD_REPLACE.txt`

---

## 🏗 Infrastructure Context

This task simulates a real-world scenario where administrators need to:
- Clean up unwanted data
- Perform controlled text replacements
- Ensure original files remain unchanged

Such operations are common in:
- Log analysis
- Configuration file updates
- Data sanitization pipelines

---

## 🧠 Key Concepts Learned

- Difference between **filtering lines** and **transforming text**
- Using `grep -v` to exclude matching lines
- Using `sed` for controlled string replacement
- Importance of **word boundaries (`\b`)**
- Safe file writing using `sudo` and `tee`
- Why direct redirection (`>`) may fail with permissions

---

## ⚙️ Commands Used

### Step 1: Connect to App Server 2
```bash
ssh steve@stapp02
hostname
```

### Step 2: Delete Lines Containing "code"
```bash
sudo grep -v code /home/BSD.txt | sudo tee /home/BSD_DELETE.txt > /dev/null
```

This removes all lines that contain the word code and saves the result.

### Step 3: Replace Exact Word "and" with "their"
```bash
sudo sed 's/\band\b/their/g' /home/BSD.txt | sudo tee /home/BSD_REPLACE.txt > /dev/null
```

This replaces only the standalone word and, not partial matches.

## 🔍 Verification Steps

```bash
cat /home/BSD_DELETE.txt
cat /home/BSD_REPLACE.txt
```

Check that:

- No lines with code exist in BSD_DELETE.txt

- Only exact and words are replaced in BSD_REPLACE.txt

- Original file /home/BSD.txt remains unchanged

## 🧩 Why Word Boundaries Matter

The pattern:
```bash
\band\b
```

Ensures:

- Matches and

- Does NOT match android, candy, standard

This prevents accidental data corruption, which is critical when working with production systems.

## ❌ Common Mistakes & Learnings

1️⃣ Using sed -i

- Modifies original file directly

- Risky in production environments

2️⃣ Forgetting Word Boundaries

- Replaces unintended parts of words

3️⃣ Using > Instead of tee

- Causes permission issues on protected paths

## 🧩 Key Takeaways

- Linux text tools are extremely powerful

- Precision is critical when manipulating data

- Always avoid modifying original files directly

- Small regex mistakes can lead to large system issues

- grep + sed + tee form a powerful data processing pipeline

## 📚 Reference Documentation

Linux manual pages:
```bash
man grep
man sed
man tee
```

## 🤝 For Learners

If you are learning Linux:

- Always test commands on sample data

- Use exact matches and boundaries

- Never modify production files blindly

- Prefer safe redirection patterns

This task represents a core Linux skill used daily by DevOps and SRE engineers.

```
⭐ If this repository helps you, consider starring it.
```