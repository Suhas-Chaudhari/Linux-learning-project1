# Question 1: Set Up Your DevOps Project Structure

## Objective

Create a complete project directory from scratch, apply correct permissions, and set ownership.

## 1. Create Project Directory Structure

Command used:

```bash
mkdir -p /home/suhas/webapp/scripts /home/suhas/webapp/logs /home/suhas/webapp/config/
```

This creates the main `/home/suhas/webapp/` directory with three subdirectories:

- `scripts/`
- `logs/`
- `config/`

## 2. Create `app.conf`

Command used:

```bash
cat > /home/suhas/webapp/config/app.conf
```

Content added:

```bash
APP_NAME=WebApp
PORT=8080
```

The file was saved using `Ctrl+D`.

Verification command:

```bash
cat /home/suhas/webapp/config/app.conf
```

Output:

```bash
APP_NAME=WebApp
PORT=8080
```

File details:

```bash
-rw-r--r-- 1 suhas suhas 26 May 10 11:13 /home/suhas/webapp/config/app.conf
```

## 3. Create Empty Log File

Command used:

```bash
touch /home/suhas/webapp/logs/app.log
```

Verification command:

```bash
ls -l /home/suhas/webapp/logs/app.log
```

Output:

```bash
-rw-r--r-- 1 suhas suhas 0 May 10 11:14 /home/suhas/webapp/logs/app.log
```

The file size is `0` bytes, so the log file is empty as required.

## 4. Set Permissions

Commands used:

```bash
chmod 755 /home/suhas/webapp/scripts
chmod 644 /home/suhas/webapp/config/app.conf
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
sudo chown -R root:root /home/suhas/webapp/
```

This changes ownership of the entire `webapp/` directory and everything inside it to user `root` and group `root`.

## 6. Final Verification

Verification command:

```bash
ls -lR /home/suhas/webapp/
```

Output:

```bash
/home/suhas/webapp/:
total 12
drwxr-xr-x 2 root root 4096 May 10 11:13 config
drwxr-xr-x 2 root root 4096 May 10 11:14 logs
drwxr-xr-x 2 root root 4096 May 10 11:11 scripts

/home/suhas/webapp/config:
total 4
-rw-r--r-- 1 root root 26 May 10 11:13 app.conf

/home/suhas/webapp/logs:
total 0
-rw-r--r-- 1 root root 0 May 10 11:14 app.log

/home/suhas/webapp/scripts:
total 0
```

## Final Result

The project structure was created successfully. The configuration file contains the required values, the log file is empty, the requested permissions were applied, and every file and directory shows `root root` as the owner and group.
