# Linux-learning-project1
# Question 1: Set Up Your DevOps Project Structure

## Objective

Create a complete project directory from scratch, apply correct permissions, and set ownership.

## 1. Create Project Directory Structure

Command used:

```bash
mkdir -p /home/ec2-user/webapp/scripts /home/ec2-user/webapp/logs /home/ec2-user/webapp/config/
```
- 
This creates the main `/home/ec2-user/webapp/` directory with three subdirectories:

- `scripts/`
- `logs/`
- `config/`

## 2. Create `app.conf`

Command used:

```bash
cat > /home/ec2-user/webapp/config/app.conf
```

Content added:

```bash
APP_NAME=WebApp
PORT=8080
```

The file was saved using `Ctrl+D`.

Verification command:

```bash
cat /home/ec2-user/webapp/config/app.conf
```

Output:

```bash
APP_NAME=WebApp
PORT=8080
```

File details:

```bash
-rw-r--r-- 1 root root 26 May 10 10:45 /home/ec2-user/webapp/config/app.conf
```

## 3. Create Empty Log File

Command used:

```bash
touch /home/ec2-user/webapp/logs/app.log
```

Verification command:

```bash
ls -l /home/ec2-user/webapp/logs/app.log
```

Output:

```bash
-rw-r--r-- 1 root root 0 May 10 10:47 /home/ec2-user/webapp/logs/app.log
```

The file size is `0` bytes, so the log file is empty as required.

## 4. Set Permissions

Commands used:

```bash
chmod 755 /home/ec2-user/webapp/scripts
chmod 644 /home/ec2-user/webapp/config/app.conf
```

### Permission Explanation

`755` means:

- Owner has read, write, and execute permission.
- Group has read and execute permission.
- Others have read and execute permission.

This is shown as:

```bash
drwxr-xr-x
```

`644` means:

- Owner has read and write permission.
- Group has read-only permission.
- Others have read-only permission.

This is shown as:

```bash
-rw-r--r--
```

## 5. Change Ownership Recursively

Command used:

```bash
chown -R root:root /home/ec2-user/webapp/
```

This changes ownership of the entire `webapp/` directory and everything inside it to user `root` and group `root`.

## 6. Final Verification

Verification command:

```bash
ls -lR /home/ec2-user/webapp/
```

Output:

```bash
/home/ec2-user/webapp/:
total 12
drwxr-xr-x 2 root root 4096 May 10 10:45 config
drwxr-xr-x 2 root root 4096 May 10 10:47 logs
drwxr-xr-x 2 root root 4096 May 10 10:43 scripts

/home/ec2-user/webapp/config:
total 4
-rw-r--r-- 1 root root 26 May 10 10:45 app.conf

/home/ec2-user/webapp/logs:
total 0
-rw-r--r-- 1 root root 0 May 10 10:47 app.log

/home/ec2-user/webapp/scripts:
total 0
```

## Final Result

The project structure was created successfully. The configuration file contains the required values, the log file is empty, the requested permissions were applied, and every file and directory shows `root root` as the owner and group.
