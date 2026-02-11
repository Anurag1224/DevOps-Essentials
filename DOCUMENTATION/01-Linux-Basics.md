# Basics of Linux Command & Shell Scripting

## Table of Contents
1. [Basic Linux Commands](#basic-linux-commands)
2. [File Operations](#file-operations)
3. [System Performance Monitoring](#system-performance-monitoring)
4. [Shell Scripting Fundamentals](#shell-scripting-fundamentals)
5. [DevOps Shell Scripting](#devops-shell-scripting)
6. [Process Management](#process-management)
7. [Pipes and Data Filtering](#pipes-and-data-filtering)
8. [Error Handling in Scripts](#error-handling-in-scripts)
9. [Control Flow Structures](#control-flow-structures)
10. [Signal Handling with Trap](#signal-handling-with-trap)
11. [Practical Examples](#practical-examples)
12. [AWS Integration](#aws-integration)

---

## Basic Linux Commands

**Note:** In Linux there is no GUI. So, we have to perform all the tasks using command line.

### Navigation Commands

**pwd** - Print Working Directory
- Shows the current directory path you are in

**ls** - List Directory Contents
- Lists all files and folders in the current directory

**cd** - Change Directory
- Changes the present working directory to another location

**Examples:**
```bash
pwd                    # Shows current path
ls                     # List files in current directory
cd /home/user          # Change to /home/user directory
cd ..                  # Move back one directory level
cd ../..               # Move back two directory levels
cd ubuntu/bundle       # Go into nested directories
```

### Listing with Details

**ls -ltr** - List with Timestamps and Properties
- Lists all files and folders with detailed information
- Shows timestamps, owner, permissions, file size, whether it's a file or directory
- Sorted by modification time (oldest first)

**ls -al** - List All Files with Full Information
- Lists all files including hidden files with complete details

---

## File Operations

### Creating Files and Directories

**mkdir** - Make Directory
- Creates a new directory/folder
- Example: `mkdir test`

**touch** - Create Empty File
- Creates an empty file
- Used most in automation
- Preferred over vi/vim when creating thousands of files
- Reason: Using vi/vim on thousands of files can slow down other processes and keep files open unnecessarily

**vi** - Visual Editor
- Creates and opens a file for editing
- Available by default on any Linux machine
- Edit mode: Press `i` after `Esc` to enter insert mode
- Save and exit: Press `Esc` then type `:wq!` and press Enter

**vim** - Improved Vi Editor
- Similar to vi but requires installation
- Offers enhanced features and user experience

**Example:**
```bash
touch filename.txt         # Create empty file
vi sample.sh              # Create and edit file
cat file.txt              # View file contents
```

### Editing and Viewing

**:wq!** - Save and Quit
- `w` = write (save)
- `q` = quit
- `!` = force operation

**cat** - Concatenate and Display
- Prints the contents of a file to the terminal
- Used to view file contents

### Removing Files and Directories

**rm** - Remove File
- Deletes a file permanently

**rm -r** - Remove Directory Recursively
- Removes a directory and all its contents
- Example: `rm -r test`

**rm -rf** - Force Remove Recursively
- Forcefully removes files and directories without confirmation
- Use with caution!

### Copying Files

**cp** - Copy Files
- Copies a file or folder to another location
- Examples:
  ```bash
  cp test.sh Desktop          # Copy to Desktop folder
  cp test.sh ..               # Copy to parent directory
  ```

### Process Management

**kill** - Terminate a Process
- Stops a running process

**kill -9 [PID]** - Force Kill
- `-9` instructs the kernel to forcefully terminate the process
- Example: `kill -9 1111`

---

## System Performance Monitoring

### Memory Monitoring

**free** - Display Memory Usage
- Shows RAM and swap memory information

**free -g** - Memory in Gigabytes
- Displays memory usage in GB format

### CPU Monitoring

**nproc** - Number of Processors
- Shows the number of CPUs allocated to the system

### Disk Space Monitoring

**df** - Disk Free Space
- Shows total, used, and available disk space

**df -h** - Disk Usage in Human-Readable Format
- Displays disk usage in KB, MB, GB format

### Comprehensive System Monitoring

**top** - System Monitoring Tool
- Shows real-time information about:
  - Memory usage
  - CPU utilization
  - Disk activity
  - Running processes
  - Resource consumption by each process

### Monitoring CPU Node Health

**Question:** How do you monitor the CPU node health?

**Answer:** Using the `top` command or custom shell scripts. Basic parameters to evaluate node health:
- **CPU** - Processor usage percentage
- **RAM** - Memory usage percentage

---

## Shell Scripting Fundamentals

### Important Commands

**man** - Manual Pages
- Displays the manual/documentation for any command
- Examples: `man ls`, `man touch`

**history** - Command History
- Shows all previously executed commands

**#** - Comment
- Used to add comments inside shell scripts
- Comments are not executed

### Shell Script File Extension

- Shell scripts use `.sh` extension
- Example: `touch first-shell-script.sh`

### Shebang (Script Header)

**#!/** - Shebang Syntax
- Specifies which shell interpreter to use
- Must be the first line of the script

**Common Shells:**
```bash
#!/bin/bash          # Bash shell (most popular and widely used)
#!/bin/dash          # Dash shell
#!/bin/sh            # Bourne shell
#!/bin/ksh           # Korn shell
```

**Important Notes:**
- Different Linux shells have slight syntax differences
- Earlier, `#!/bin/sh` and `#!/bin/bash` were linked, but not anymore
- Some OS use dash as default, which may cause bash scripts to fail
- Ubuntu machines should use `#!/bin/bash`

### Printing Output

**echo** - Print Statement
- Similar to `print` in Python and `cout` in C++
- Displays text to the terminal

```bash
echo "Hello I am Anurag"
echo $VARIABLE_NAME
```

### Executing Scripts

**sh** - Execute Shell Script
- Runs a shell script file
- Example: `sh test.sh`

**./** - Execute Any Executable File
- Runs any executable (Python, C++, shell scripts, etc.)
- Example: `./test_python.py` or `./script.sh`

### File Permissions and Execution

**Important:** By default, when you create a file, you have read and write permissions but NOT execute permission. You need to change permissions to run the script.

**chmod** - Change File Mode (Permissions)
- Grants permissions to a file
- Changes the mode/access rights

### Permission Categories

There are 3 categories for permissions:
1. **user** (owner of the file)
2. **group** (group that owns the file)
3. **everyone** (other users)

### Permission Values

- **4** = Read only
- **2** = Write only
- **1** = Execute only
- **Combinations:**
  - **7** = Read + Write + Execute (4+2+1)
  - **6** = Read + Write (4+2)
  - **5** = Read + Execute (4+1)

### Permission Format

```
chmod 764 filename

Position 1 (7): User/Owner permissions     (read+write+execute)
Position 2 (6): Group permissions          (read+write)
Position 3 (4): Everyone/Other permissions (read)
```

**Examples:**
```bash
chmod 777 test.sh              # Everyone has full permissions
chmod 744 test.sh              # Owner has full, others can read & execute
chmod 755 script.sh            # Standard for executable scripts
chmod 600 config.sh            # Only owner can read and write

# Alternative notation:
chmod u+x test.sh              # Give user execute permission
chmod g+w test.sh              # Give group write permission
chmod o+w test.sh              # Give others write permission
```

### Copying Content in Terminal

- Double-click to select and copy content
- Paste with `Ctrl+V` (Windows/Linux) or `Cmd+V` (Mac)

---

## Shell Scripting Fundamentals - Example Script

**Example: Creating and Running Your First Script**

```bash
#!/bin/bash

# Create a folder named test
mkdir test

# Move into the test directory
cd test

# Create two files inside the test directory
touch firstFile secondFile
```

**Steps to execute:**
1. Create script: `vi sample-shell-script.sh`
2. Paste the above code
3. Save: Press `Esc`, then type `:wq!`, press Enter
4. Change permissions: `chmod 744 sample-shell-script.sh`
5. Execute: `./sample-shell-script.sh`

---

## DevOps Shell Scripting

### Why We Need Shell Scripting

Shell scripting is essential for DevOps engineers in day-to-day operations for:
- Infrastructure maintenance
- Configuration management
- Monitoring and health checks
- Automation of repetitive tasks
- Log analysis and troubleshooting

**Note:** While tools like Ansible exist for configuration management, shell scripting provides:
- More detailed insights into machine health
- Greater flexibility and control
- Better understanding of system behavior

### Debug Mode

**set -x** - Enable Debug Mode
- Runs commands in debug mode
- Prints each command before executing it
- Extremely helpful for troubleshooting scripts
- Helps DevOps engineers identify and fix issues quickly

**Example Script with Debug Mode:**

```bash
#!/bin/bash
####################
# Author: Anurag
# Date: 09/12/2025
#
# This script outputs the node health
#
# Version: v1
####################

set -x

df -h              # Display disk usage
free -g            # Display memory in GB
nproc              # Display number of CPUs
```

### Best Practices for Scripts

- Always write metadata information (Author, Date, Version)
- Whenever starting a script, use `set -x` for debug mode
- You can combine `set -x` with echo statements based on requirements
- For large scripts, using only echo statements is not feasible
- If you don't want users to see certain commands, comment them out

---

## Process Management

### Listing Processes

**ps** - Process Status
- Lists currently running processes

**ps -ef** - All Running Processes
- Displays all processes running on the VM (not just background)
- `-e`: Selects all processes running on the system
- `-f`: Provides full-format listing with additional details

**Uses of ps -ef:**
- Process Management: View and understand running processes
- Troubleshooting: Identify processes consuming high CPU or memory
- System Monitoring: Gain insights into resource usage and application activity

**ps -ef | grep "amazon"** - Filter Specific Processes
- Lists only processes running by the "amazon" user/application

---

## Pipes and Data Filtering

### The Pipe (|) Operator

**Pipe (|)** - Command Chaining Operator
- Sends the output of one command as input to another
- Allows chaining multiple commands together
- Example: `ps -ef | grep nginx`

**Important:** Pipe only works with stdout. It cannot receive input from stdin.

### Important Concept: stdin, stdout, stderr

In any system, there are three data channels:
1. **stdin** - Standard Input
2. **stdout** - Standard Output
3. **stderr** - Standard Error

**Example - Why This Doesn't Work As Expected:**

```bash
date | echo "date is"
# Expected output: date is Fri Dec 5 06:12:55 UTC 2025
# Actual output: date is
```

**Reason:** The `date` command sends output to stdin, but pipe expects stdout. Therefore, only "date is" is printed.

### grep - Pattern Matching and Filtering

**grep** - Search Text Patterns
- Prints lines matching special patterns
- Filters output based on search criteria

**Example:**
```bash
ps -ef | grep nginx

# Output:
# root        3776       1  0 Dec03 ?        00:00:00 nginx: master process
# www-data    3778    3776  0 Dec03 ?        00:00:00 nginx: worker process
# www-data    3779    3776  0 Dec03 ?        00:00:00 nginx: worker process
# ubuntu     58404   58163  0 13:14 pts/0    00:00:00 grep --color=auto nginx
```

### awk - Advanced Text Processing

**awk** - Pattern Scanning and Processing Language
- Much more powerful than grep
- Can filter and extract specific columns from output
- Uses field separators to identify columns

**Key Difference between grep and awk:**
- **grep**: Returns the entire matching line
- **awk**: Filters the line and extracts specific columns

**Example with Field Separator:**

```bash
ps -ef | grep "nginx" | awk -F" " '{print $2}'

# Output:
# 3776
# 3778
# 3779
# 58411

# -F" " means field separator is space
# {print $2} means print the 2nd column (process ID)
```

**Another Example:**

```bash
# File: test.txt
# My name is Anurag.
# I work in Microsoft.

grep "name" test.txt
# Output: My name is Anurag.

grep "name" test.txt | awk -F" " '{print $4}'
# Output: Anurag.
```

**Important Notes:**
- Always verify you're using the correct column number
- Ensure grep is applied to the right data
- Use appropriate field separators based on your data format

---

## Error Handling in Scripts

### Error Exit Handling

**set -e** - Exit on Error
- Exits the script when an error occurs
- Does NOT catch errors from pipes (only the last command status)

**set -o pipefail** - Catch Pipe Failures
- Exits if any command in a pipe fails
- Ensures all commands in a pipeline are checked for errors

**Example Scenarios:**

```bash
# Without set -o pipefail:
Sdfgh | echo | fghjk
# Only checks if fghjk succeeds, ignores Sdfgh and echo errors

# With set -o pipefail:
Sdfgh | echo | fghjk
# Exits on first error (Sdfgh)
```

### Proper Error Handling Pattern

```bash
#!/bin/bash

set -x           # Debug mode
set -e           # Exit on error
set -o pipefail  # Exit on pipe failure
```

**Important:** Write these separately for flexibility. Combining as `set -exo pipefail` is less readable.

```bash
# Good practice:
set -x              # Enable debugging
set -e              # Exit on error
set -o pipefail     # Catch pipe failures
```

---

## Control Flow Structures

### If-Else Statement

**Syntax:**
```bash
if [expression]
then
    # Commands if condition is true
else
    # Commands if condition is false
fi              # Marks the end of if statement
```

**Example:**
```bash
#!/bin/bash

a=4
b=10

if [ $a -gt $b ]
then
    echo "a is greater than b"
else
    echo "b is greater than a"
fi
```

### For Loop

**Syntax:**
```bash
for i in {start..end}
do
    # Commands to execute
    echo $i
done
```

**Example:**
```bash
for i in {1..10}
do
    echo "Number: $i"
done
```

---

## Signal Handling with Trap

### Understanding Signals

**Signal** - A notification sent to a process
- Example: Pressing `Ctrl+C` sends a SIGINT signal
- Each signal has a numeric ID and name
- Linux has multiple built-in signals

### Common Linux Signals

| Signal | Description |
|--------|-------------|
| **SIGINT** | Generated when user presses Ctrl+C; terminates program |
| **SIGALRM** | Generated when timer set by alarm function goes off |
| **SIGABRT** | Generated when process executes abort function |
| **SIGSTOP** | Tells Linux to pause a process to be resumed later |
| **SIGCONT** | Tells Linux to resume a paused process |
| **SIGSEGV** | Sent when process has a segmentation fault |
| **SIGKILL** | Sent to cause a process to terminate immediately |

### The trap Command

**trap** - Signal and Exit Handler
- Allows defining actions when shell receives specific signals
- Can intercept SIGINT, SIGTERM, SIGHUP, and other signals
- Executes defined commands instead of default signal action
- Enables graceful handling of interruptions and cleanup operations

**Syntax:**
```bash
trap "command_to_execute" SIGNAL_NAME
```

**Example 1: Prevent Ctrl+C**
```bash
trap "echo 'You cannot use Ctrl+C!'" SIGINT
```

**Example 2: Cleanup on Ctrl+C**
```bash
#!/bin/bash

# Database population script
trap "rm -rf *; echo 'Cleanup completed'" SIGINT

# Your database population commands here
```

**Use Case:**
Suppose a script populates a database. If someone presses Ctrl+C halfway through, only partial data is saved. With trap, you can delete incomplete data or perform proper cleanup when interrupted.

---

## Practical Examples

### Example 1: Print Numbers Divisible by 3 and 5 (but not 15)

**Problem:** Write a script to print numbers from 1 to 100 that are divisible by 3 and 5 but NOT by 15.

```bash
#!/bin/bash
####################
# Author: Anurag
# Date: 09/12/2025
#
# This script outputs numbers divisible by 3 and 5 but not 15 (1-100)
#
# Version: v1
####################

for i in {1..100}
do
    if (( (i % 3 == 0 || i % 5 == 0) && i % 15 != 0 ))
    then
        echo $i
    fi
done
```

### Example 2: Count Character Occurrences

**Problem:** Write a script to count how many 's' characters are in the word "mississippi".

```bash
#!/bin/bash
####################
# Author: Anurag
# Date: 09/12/2025
#
# This script counts the letter 's' in the word mississippi
#
# Version: v1
####################

x="mississippi"

grep -o "s" <<<"$x" | wc -l
```

**Explanation:**
- `-o` flag: Output only matching parts
- `<<<` (here string): Redirects string to stdin of grep
- `wc -l`: Counts lines (each 's' is on a separate line)

---

## AWS Integration

### Project 1: AWS Resource Tracker Script

**Objective:** Create a script that reports AWS resource usage (S3, EC2, Lambda, IAM)

```bash
#!/bin/bash
####################
# Author: Anurag
# Date: 09/12/2025
#
# This script will report the AWS resource usage
#
# Version: v1
####################

# Run the script in debug mode
set -x

# List S3 buckets
echo "Print the list of S3 buckets"
aws s3 ls

# Store S3 buckets to file (overwrite)
echo "Print the list of S3 buckets and store the output in resourceTracker"
aws s3 ls > resourceTracker

# List EC2 Instances
echo "Print the list of EC2 instances"
aws ec2 describe-instances

# Extract specific Instance IDs from JSON output
echo "Get the particular Instance ID from JSON"
aws ec2 describe-instances | jq 'Reservations[].Instances[].InstanceId'

# List Lambda functions and append to file
echo "Print the list of lambda functions"
aws lambda list-functions >> resourceTracker

# List IAM users
echo "Print the list of IAM users"
aws iam list-users
```

**Prerequisites:**
- AWS CLI installed and configured
- Appropriate AWS IAM permissions
- `jq` for JSON parsing

**Key Commands:**
- `aws s3 ls` - List all S3 buckets
- `aws ec2 describe-instances` - Get EC2 instance details
- `jq` - JSON query tool for parsing structured output
- `aws lambda list-functions` - List Lambda functions
- `aws iam list-users` - List IAM users

**Output:**
- S3 bucket list saved to `resourceTracker` file
- Lambda functions appended to `resourceTracker` file
- All operations executed in debug mode for visibility

---

## Summary

This guide covers the essential Linux commands and shell scripting concepts needed for DevOps work. Key takeaways:

✅ Master basic file and directory operations
✅ Monitor system performance using appropriate tools
✅ Write clean, well-documented shell scripts
✅ Use proper error handling with set -e and set -o pipefail
✅ Leverage pipes, grep, and awk for powerful data filtering
✅ Handle signals gracefully with trap
✅ Integrate shell scripts with AWS for infrastructure automation
✅ Always include metadata and use debug mode during development

---

**Author:** Anurag  
**Date:** 09/12/2025  
**Version:** v1.0

*For more advanced topics, refer to the additional shell scripting guide.*

