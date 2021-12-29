## Week 5 Homework Submission File: Archiving and Logging Data

Please edit this file by adding the solution commands on the line below the prompt.

Save and submit the completed file for your homework submission.

---

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives

1. Command to **extract** the `TarDocs.tar` archive to the current directory: sudo tar xvf TarDocs.tar

2. Command to **create** the `Javaless_Doc.tar` archive from the `TarDocs/` directory, while excluding the `TarDocs/Documents/Java` directory: sudo tar cvf Javaless_Docs.tar --exclude="TarDocs/Documents/Java" TarDocs/

3. Command to ensure `Java/` is not in the new `Javaless_Docs.tar` archive: sudo tar tvf Javaless_Docs.tar | grep Java

**Bonus**
- Command to create an incremental archive called `logs_backup_tar.gz` with only changed files to `snapshot.file` for the `/var/log` directory: sudo tar cvf logs_backup_tar.gz --listed-incremental=logs_backup_snapshot.snar /var/log

#### Critical Analysis Question

- Why wouldn't you use the options `-x` and `-c` at the same time with `tar`?
      - You would not use -x and -c simultaneously with tar because these options have different objectives. The -x option allows the user to extract a tar file, whereas a -c option allows a user to create a tar file. You would need to run separate tar commands in order to both create a tar file, then extract the file (or vise versa). You could hypothetically extract a tar file then create a new one, but this would be superfluous unless there were additional filters created on the newly created tar file, otherwise you'd be creating a duplicate tar file.
---

### Step 2: Create, Manage, and Automate Cron Jobs

1. Cron job for backing up the `/var/log/auth.log` file:

# Homework Week 5
0 6 * * 3 tar cvf auth_backup.tgz /var/log/auth.log

---

### Step 3: Write Basic Bash Scripts

1. Brace expansion command to create the four subdirectories: mkdir -p backups/{freemem,diskuse,openlist,freedisk}

2. Paste your `system.sh` script edits below:

    ```bash
    #!/bin/bash
    free mem -h > ~/backups/freemem/free_mem.txt
    df -h --output=source,size,used,pcent  > ~/backups/diskuse/disk_usage.txt
    lsof > ~/backups/openlist/open_list.txt
    df -h --output=source,size,avail > ~/backups/freedisk/free_disk.txt
    ```

3. Command to make the `system.sh` script executable: chmod +x system.sh

**Optional**
- Commands to test the script and confirm its execution:
sudo ./system.sh | ls /home/sysadmin/backups/*
or
cat /home/sysadmin/backups/freedisk/freedisk.txt && cat /home/sysadmin/backups/openlist/openlist.txt && cat /home/sysadmin/backups/freemem/freemem.txt && cat /home/sysadmin/backups/diskuse/diskuse.txt

**Bonus**
- Command to copy `system` to system-wide cron directory:

sudo cp ~/system.sh /etc/cron.weekly/

---

### Step 4. Manage Log File Sizes

1. Run `sudo nano /etc/logrotate.conf` to edit the `logrotate` configuration file.

    Configure a log rotation scheme that backs up authentication messages to the `/var/log/auth.log`.

    - Add your config file edits below:

    ```bash
    # Homework 5 Logrotate
    /var/log/auth.log {
            weekly
            rotate 7
            notifempty
            delaycompress
            missingok
    }
    ```
---

### Bonus: Check for Policy and File Violations

1. Command to verify `auditd` is active: systemctl status auditd

2. Command to set number of retained logs and maximum log file size:

    - Add the edits made to the configuration file below:

    ```bash
    max_log_file = 35
    num_logs = 7
    ```

3. Command using `auditd` to set rules for `/etc/shadow`, `/etc/passwd` and `/var/log/auth.log`:


    - Add the edits made to the `rules` file below:

    ```bash
    # Homework 5 Audit
    -w /etc/shadow -p wa -k hashpass_audit
    -w /etc/passwd -p wa -k userpass_audit
    -w /var/log/auth.log -p wa -k authlog_audit
    ```

4. Command to restart `auditd`: systemctl restart auditd

5. Command to list all `auditd` rules: sudo auditctl -l

6. Command to produce an audit report: sudo aureport -au

7. Create a user with `sudo useradd attacker` and produce an audit report that lists account modifications: sudo aureport -m

8. Command to use `auditd` to watch `/var/log/cron`: sudo auditctl –w /var/log/cron

9. Command to verify `auditd` rules: sudo aureport -m
or
sudo auditctl -l

---

### Bonus (Research Activity): Perform Various Log Filtering Techniques

1. Command to return `journalctl` messages with priorities from emergency to error: journalctl -ef -p err -b

1. Command to check the disk usage of the system journal unit since the most recent boot: journalctl --disk-usage

1. Command to remove all archived journal files except the most recent two: sudo journalctl --vacuum-files=2

1. Command to filter all log messages with priority levels between zero and two, and save output to `/home/sysadmin/Priority_High.txt`: journalctl -p crit -b >> /home/sysadmin/Priority_High.txt

1. Command to automate the last command in a daily cronjob. Add the edits made to the crontab file below:

    ```bash
0 6 * * * journalctl -p crit -b >> /home/sysadmin/Priority_High.txt
    ```

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
