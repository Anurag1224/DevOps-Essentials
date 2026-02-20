📧 Day 33 – Postfix Service Troubleshooting
# 📧 Day 33 – Postfix Service Troubleshooting

## 📌 Task Overview

The monitoring team reported that the mail server in Stork DC was not functioning properly. The Postfix service was failing to start.

**Objectives:**
- Identify the root cause
- Fix the configuration
- Restore Postfix service successfully

**Mail Server Details:**
- **Host:** stmail01
- **MTA:** Postfix

## 🛠 Initial Problem

When attempting to start the service:

```bash
sudo systemctl start postfix
```

The service failed. Checking status:

```bash
sudo systemctl status postfix
```

**Key error in logs:**

```
fatal: parameter inet_interfaces: no local interface found for ::1
warning: overriding earlier entry: inet_interfaces=all
```

## 🔍 Root Cause Analysis

Two configuration problems were identified in `/etc/postfix/main.cf`:

### 1️⃣ Duplicate Parameter Entry

The parameter `inet_interfaces` was defined more than once in the file.

Postfix warning:
```
overriding earlier entry
```

This indicates configuration inconsistency.

### 2️⃣ IPv6 Binding Issue

Postfix was attempting to bind to:
- `::1` (IPv6 loopback address)

However, the lab/container environment does not support IPv6, causing startup failure.

## 🧠 Understanding the Key Parameters

### `inet_interfaces`
Defines which network interfaces Postfix listens on.

```
inet_interfaces = all
```

### `inet_protocols`
Defines whether Postfix uses IPv4, IPv6, or both. Default behavior may attempt both IPv4 and IPv6, causing failures in IPv6-less environments.

## ✅ Solution Implemented

### Step 1 – Edit Configuration File

```bash
sudo vi /etc/postfix/main.cf
```

### Step 2 – Remove Duplicate Entry

Ensured only one definition of `inet_interfaces`.

### Step 3 – Restrict to IPv4 Only

Updated configuration:

```
inet_interfaces = all
inet_protocols = ipv4
```

⚠️ **Important:** `ipv4` must be lowercase.

## 🔎 Configuration Validation

Before restarting the service:

```bash
sudo postfix check
```

**Expected result:**
- No output
- No errors

## 🚀 Restarting Postfix

```bash
sudo systemctl restart postfix
sudo systemctl status postfix
```

**Service status:**
```
Active: active (running)
```

## 🧪 Verification

Confirmed Postfix is listening on port 25:

```bash
ss -tulnp | grep :25
```

**Output showed:**
```
0.0.0.0:25
```

This confirms Postfix is successfully bound to IPv4.

## 📚 Key Learnings

- Logs are the first place to look during service failures
- Duplicate configuration entries can override earlier settings
- IPv6 misconfiguration is common in containerized environments
- Always validate configuration before restarting services
- `postfix check` is critical before applying changes

## 🧠 Troubleshooting Workflow Used

1. Check service status
2. Inspect logs
3. Identify fatal parameter
4. Review configuration file
5. Fix environment-specific issue
6. Validate
7. Restart and verify

## 🎯 Final Outcome

✅ Root cause identified correctly  
✅ Configuration fixed  
✅ Postfix service restored  
✅ Mail server operational again
