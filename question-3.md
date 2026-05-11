# Question 3: User Management and File Permission Control

## Objective

Create 4 Linux users. Give write access to `devuser1` and `devuser2` using the `writers` group. Give read-only access to `devuser3` and `devuser4` using file permissions.

## Step 1: Create the Group

Command:

```bash
sudo groupadd writers
```

Explanation:

This creates a Linux group named `writers`. Users inside this group will be allowed to write to `log_user.sh`.

Screenshot verification:

```bash
root@os:~# sudo groupadd writers
```

## Step 2: Create 4 Users with Home Directories

Commands:

```bash
sudo useradd -m devuser1
sudo useradd -m devuser2
sudo useradd -m devuser3
sudo useradd -m devuser4
```

Explanation:

The `-m` option creates a home directory for each user.

Verification commands:

```bash
tail /etc/passwd
ls -ltr /home
```

Screenshot output showed the users were created:

```bash
devuser1:x:1001:1002::/home/devuser1:/bin/sh
devuser2:x:1002:1003::/home/devuser2:/bin/sh
devuser3:x:1003:1004::/home/devuser3:/bin/sh
devuser4:x:1004:1005::/home/devuser4:/bin/sh
```

Screenshot output also showed home directories for:

```bash
devuser1
devuser2
devuser3
devuser4
suhas
```

## Password Setup

Commands:

```bash
sudo passwd devuser1
sudo passwd devuser2
sudo passwd devuser3
sudo passwd devuser4
```

Screenshot output:

```bash
passwd: password updated successfully
passwd: password updated successfully
passwd: password updated successfully
passwd: password updated successfully
```

## Step 3: Add Write-Access Users to the `writers` Group

Commands:

```bash
sudo usermod -aG writers devuser1
sudo usermod -aG writers devuser2
```

Explanation:

`devuser1` and `devuser2` are added to the `writers` group. These two users will get write access to the script.

## Step 4: Change Group Ownership of the Script

Command:

```bash
sudo chown root:writers /home/suhas/webapp/scripts/log_user.sh
```

Explanation:

This keeps `root` as the owner of the file and changes the group owner to `writers`.

Verification command:

```bash
ls -ltr /home/suhas/webapp/scripts/log_user.sh
```

Screenshot output:

```bash
-rwxr-xr-- 1 root writers 201 May 10 11:33 /home/suhas/webapp/scripts/log_user.sh
```

## Step 5: Set File Permissions to `664`

Command:

```bash
sudo chmod 664 /home/suhas/webapp/scripts/log_user.sh
```

Verification command:

```bash
ls -ltr /home/suhas/webapp/scripts/log_user.sh
```

Screenshot output:

```bash
-rw-rw-r-- 1 root writers 201 May 10 11:33 /home/suhas/webapp/scripts/log_user.sh
```

Explanation:

`664` means:

- Owner `root`: read and write
- Group `writers`: read and write
- Others: read only

Permission layout:

```text
6 = owner has read and write
6 = group has read and write
4 = others have read only
```

## Step 6: Verify Permissions

Command:

```bash
ls -l /home/suhas/webapp/scripts/log_user.sh
```

Expected output:

```bash
-rw-rw-r-- 1 root writers 201 May 10 11:33 /home/suhas/webapp/scripts/log_user.sh
```

This confirms:

- `root` is the owner
- `writers` is the group
- Owner and group have read/write access
- Others have read-only access

## Step 7: Test Write Access for `devuser1`

Commands:

```bash
su - devuser1
echo 'test from devuser1' >> /home/suhas/webapp/scripts/log_user.sh
exit
```

Screenshot output:

```bash
$ echo 'test from devuser1' >> /home/suhas/webapp/scripts/log_user.sh
$ exit
logout
```

Explanation:

Since `devuser1` is in the `writers` group, this user should be able to append text to the file.

## Step 8: Test Write Access for `devuser2`

Commands:

```bash
su - devuser2
echo 'test from devuser2' >> /home/suhas/webapp/scripts/log_user.sh
exit
```

Screenshot output:

```bash
$ echo 'test from devuser2' >> /home/suhas/webapp/scripts/log_user.sh
$ exit
logout
```

Explanation:

Since `devuser2` is also in the `writers` group, this user should also be able to write to the file.

## Step 9: Test Read-Only Access for `devuser3`

Commands:

```bash
su - devuser3
cat /home/suhas/webapp/scripts/log_user.sh
echo 'test from devuser3' >> /home/suhas/webapp/scripts/log_user.sh
exit
```

Screenshot output:

```bash
$ echo 'test from devuser3' >> /home/suhas/webapp/scripts/log_user.sh
-sh: 1: cannot create /home/suhas/webapp/scripts/log_user.sh: Permission denied
```

Expected result:

The `cat` command should work, but the `echo >>` command should fail with `Permission denied`.

## Step 10: Test Read-Only Access for `devuser4`

Commands:

```bash
su - devuser4
cat /home/suhas/webapp/scripts/log_user.sh
echo 'test from devuser4' >> /home/suhas/webapp/scripts/log_user.sh
exit
```

Screenshot output:

```bash
$ echo 'test from devuser4' >> /home/suhas/webapp/scripts/log_user.sh
-sh: 1: cannot create /home/suhas/webapp/scripts/log_user.sh: Permission denied
```

Expected result:

The `cat` command should work, but the `echo >>` command should fail with `Permission denied`.

## Screenshot Evidence Summary

The screenshot verifies the following:

- The `writers` group was created.
- `devuser1`, `devuser2`, `devuser3`, and `devuser4` were created with home directories.
- Passwords were set successfully for all four users.
- `devuser1` and `devuser2` were added to the `writers` group.
- `log_user.sh` ownership was changed to `root:writers`.
- File permissions were changed to `664`, shown as `-rw-rw-r--`.
- `devuser1` and `devuser2` were able to append text to `log_user.sh`.
- `devuser3` and `devuser4` were able to read the file but received `Permission denied` when trying to write.

## Final Verification

Command:

```bash
ls -l /home/suhas/webapp/scripts/log_user.sh
```

Expected final output:

```bash
-rw-rw-r-- 1 root writers 201 May 10 11:33 /home/suhas/webapp/scripts/log_user.sh
```

## Final Result

The `writers` group was created successfully. Four users were created. `devuser1` and `devuser2` were added to the `writers` group and can write to `log_user.sh`. `devuser3` and `devuser4` are not in the group, so they can only read the file.
