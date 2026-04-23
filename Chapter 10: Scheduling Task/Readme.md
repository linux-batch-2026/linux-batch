# ⏰ Scheduling Tasks 

Linux allows scheduling tasks using **cron** (recurring jobs) and **at** (one-time jobs).

### 1. **Cron Jobs (Recurring Tasks)**

Cron jobs are defined in crontab files.

**Syntax:**

```
* * * * * command_to_execute
- - - - -
| | | | |
| | | | +---- Day of week (0 - 7) (Sunday=0 or 7)
| | | +------ Month (1 - 12)
| | +-------- Day of month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)
```

**Examples:**

* Run script every day at midnight:

```bash
0 0 * * * /home/user/backup.sh
```

* Run job every Monday at 3 AM:

```bash
0 3 * * 1 /home/user/weekly_report.sh
```

* Run job every 5 minutes:

```bash
*/5 * * * * /home/user/monitor.sh
```

**Manage Crontab:**

* `crontab -e` → Edit crontab.
* `crontab -l` → List jobs.
* `crontab -r` → Remove all jobs.

---

### 2. **At Command (One-Time Task)**

The `at` command is used for scheduling tasks at a specific time.

**Examples:**

* Run job at 10:30 PM today:

```bash
echo "/home/user/cleanup.sh" | at 22:30
```

* Run job tomorrow at 5 AM:

```bash
echo "reboot" | at 5am tomorrow
```

* Run job two days later:

```bash
echo "tar -czf backup.tar.gz /home/user" | at now + 2 days
```

**Manage At Jobs:**

* `atq` → List scheduled jobs.
* `atrm <job_id>` → Remove a scheduled job.

---

