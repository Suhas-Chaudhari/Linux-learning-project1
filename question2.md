# Question 2: Write an Interactive Log Script

## Objective

Using the `webapp/` structure from Question 1, create a bash script that takes user input, reads the application config file, and writes timestamped login entries to the application log file.

## 1. Navigate to the Scripts Directory

Command used:

```bash
cd /home/suhas/webapp/scripts/
```

## 2. Create the Script with `vim`

Command used:

```bash
vim log_user.sh
```

Inside `vim`, press `i` to enter insert mode, then add the following script:

```bash
#!/bin/bash
read -p "Enter your name: " username
cat /home/suhas/webapp/config/app.conf
echo "Login: $username Date: $(date)" >> /home/suhas/webapp/logs/app.log
cat /home/suhas/webapp/logs/app.log
```

To save and exit:

```bash
Esc
:wq
Enter
```

## 3. Give Execute Permission

Command used:

```bash
chmod +x log_user.sh
```

Verification command:

```bash
ls -l log_user.sh
```

Expected output:

```bash
-rwxr-xr-x 1 root root 207 May 10 12:00 log_user.sh
```

The `x` permission means the script can be executed.

## 4. Run the Script Three Times

Run the script:

```bash
./log_user.sh
```

Example run 1:

```bash
root@suhchaud-33034929H:/home/suhas/webapp/scripts# ./log_user.sh
Enter your name: Suhas
APP_NAME=WebApp
PORT=8080
Login: Suhas Date: Sun May 10 11:35:42 UTC 2026
```

Check the log file:

```bash
root@suhchaud-33034929H:/home/suhas/webapp/scripts# cat /home/suhas/webapp/logs/app.log
Login: Suhas Date: Sun May 10 11:35:42 UTC 2026
```

Example run 2:

```bash
root@suhchaud-33034929H:/home/suhas/webapp/scripts# ./log_user.sh
Enter your name: reeva
APP_NAME=WebApp
PORT=8080
Login: Suhas Date: Sun May 10 11:35:42 UTC 2026
Login: reeva Date: Sun May 10 11:40:24 UTC 2026
```

Example run 3:

```bash
root@suhchaud-33034929H:/home/suhas/webapp/scripts# ./log_user.sh
Enter your name: Ajit
APP_NAME=WebApp
PORT=8080
Login: Suhas Date: Sun May 10 11:35:42 UTC 2026
Login: reeva Date: Sun May 10 11:40:24 UTC 2026
Login: Ajit Date: Mon May 11 09:38:08 UTC 2026
```

## 5. Check the Log File

Command used:

```bash
cat /home/suhas/webapp/logs/app.log
```

Expected output:

```bash
Login: Suhas Date: Sun May 10 11:35:42 UTC 2026
Login: reeva Date: Sun May 10 11:40:24 UTC 2026
Login: Ajit Date: Mon May 11 09:38:08 UTC 2026
```

## Final Result

The `log_user.sh` script was created successfully. It prompts the user for a name, displays the application configuration, appends a timestamped login entry to `logs/app.log`, and displays the full log file contents. The script was given execute permission and run three times with different names, so the log file contains multiple entries for Question 3.
