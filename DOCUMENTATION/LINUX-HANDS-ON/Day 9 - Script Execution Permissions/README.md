text
# Linux Hands-On Practice – Day 9
## Script Execution Permissions (Linux Level 1)

This document captures **Day 9 learning** from the **KodeKloud Engineer – Nautilus Project** as part of my **DevOps journey**. Focus: Making scripts executable for automation workflows.

---

## 📋 Task Overview

**Task Name:** Script Execution Permissions  
**Level:** Linux Level 1  
**Datacenter:** Stratos  
**Target Server:** App Server 1 (`stapp01`)

### 🎯 Objectives
- Locate `/tmp/xfusioncorp.sh`
- Make script executable for **all users**
- Verify permissions work correctly

---

## 🏗️ Real-World Context

**Scenario:** Backup script deployed via CI/CD pipeline fails to execute due to missing execute permissions.

**Common Causes:**
- Files transferred via `scp`/`rsync` lose execute bit
- Scripts created by automation tools without `+x`
- Container images with permission mismatches

---

## 🔍 Initial State Check

```bash
ls -l /tmp/xfusioncorp.sh
```
```
Output: -rw-r--r-- 1 root root ...
```
Problem: No x (execute) bit set → Script won't run

## ✅ Solution Methods

Method 1: Quick Fix (Recommended)
```bash
sudo chmod a+x /tmp/xfusioncorp.sh
```
What it does: Adds execute permission for owner/group/others

Method 2: Numeric Mode (755)
```bash
sudo chmod 755 /tmp/xfusioncorp.sh
```
Breakdown: 7=owner(rwx), 5=group(rx), 5=others(rx)

Method 3: Specific User Targeting
```bash
# Owner only
sudo chmod u+x /tmp/xfusioncorp.sh

# Owner + Group
sudo chmod ug+x /tmp/xfusioncorp.sh

# Everyone (same as +x)
sudo chmod a+x /tmp/xfusioncorp.sh
```
## 🔬 Verification
```bash
ls -l /tmp/xfusioncorp.sh
```
Success Output: -rwxr-xr-x 1 root root ...
✅ All users can now execute


## 💡 Key Takeaways

- Execute bit (x) is mandatory for script execution

- ermissions ≠ File content – readable ≠ executable

- chmod +x = safest way to enable execution

- Always verify with ls -l before running

- 755 = industry standard for production scripts

## 🔗 Quick Reference Commands
```bash
### Permission cheat sheet
chmod +x file          # Everyone can execute
chmod 755 file         # Standard script perms
chmod u+x file         # Owner only
chmod ug+x file        # Owner + group
ls -l file             # Check permissions
file file.sh           # Verify it's a script
```
## 📚 References
```bash
man chmod

man ls
```
Linux Permission Bits Explained

