# Day 8 - Data Backup for Developer

## Overview
In today's task, we will learn how to create a compressed archive of a developer's data and transfer it to a specified directory. This process is essential for data backup and management in a development environment.

## Task Details
Developer **James** has requested a backup of their non-confidential data stored in the directory `/data/james`. We will follow the steps provided by the System Admin team to fulfill this request.

## Steps to Complete the Task

### Step 1: Create a Compressed Archive
To create a compressed archive of the `/data/james` directory, we will use the `tar` command. Open your terminal and execute the following command:

```bash
tar -czvf james.tar.gz /data/james
```

- `tar`: The command used to create the archive.
- `-c`: Create a new archive.
- `-z`: Compress the archive using gzip.
- `-v`: Verbosely list files processed.
- `-f`: Specify the name of the archive file.

### Step 2: Transfer the Archive
Once the archive is created, we need to transfer it to the `/home` directory on the Storage Server. Use the following command:

```bash
mv james.tar.gz /home/
```

This command moves the `james.tar.gz` file to the `/home` directory.

## Conclusion
By following these steps, you have successfully created a backup of Developer James's data and transferred it to the appropriate directory. This process is crucial for ensuring data safety and accessibility in a development environment.

## Alternative Method
You can also perform this task using separate commands for creating, compressing, and moving the archive:

```bash
cd /data
sudo tar -cf james.tar james
sudo gzip james.tar
sudo mv james.tar.gz /home/
```

- `cd /data`: Navigate to the data directory.
- `sudo tar -cf james.tar james`: Create an uncompressed archive named `james.tar`.
- `sudo gzip james.tar`: Compress the archive using gzip, creating `james.tar.gz`.
- `sudo mv james.tar.gz /home/`: Move the compressed archive to the `/home` directory.

This method gives you more control over each step of the backup process.



