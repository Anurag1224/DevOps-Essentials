# Day 5 – Temporary User with Expiry Date

## Objective
Create a temporary user account with an expiry date for limited-duration project access.

## Task Overview
Set up a temporary user named `anita` on App Server 2 in Stratos Datacenter with an account expiry date of **2027-02-17**.

## Prerequisites
- Access to App Server 2 in Stratos Datacenter
- Root or sudo privileges
- Infrastructure details from the Nautilus project

## Steps

### 1. Connect to App Server 2
Access the target server using SSH or the provided console.

### 2. Create the User Account
```bash
sudo useradd -m anita
```
- `-m`: Creates the user's home directory

### 3. Set the Account Expiry Date
```bash
sudo usermod -e 2027-02-17 anita
```
- `-e`: Sets the account expiry date in YYYY-MM-DD format

### 4. Verify the Configuration
```bash
sudo chage -l anita
```
This displays the password aging information including the expiry date.

## Alternative: Create User with Expiry in One Command
```bash
sudo useradd -m -e 2027-02-17 anita
```

## Key Notes
- Username must be lowercase (`anita`)
- Expiry date format: `YYYY-MM-DD`
- After expiry, the user cannot log in
- Home directory is created automatically with `-m` flag

## Reference
[Kodekloud Nautilus Infrastructure Details](https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details)

## Commands Summary
| Command | Purpose |
|---------|---------|
| `useradd -m anita` | Create user with home directory |
| `usermod -e 2027-02-17 anita` | Set expiry date |
| `chage -l anita` | Verify expiry configuration |
