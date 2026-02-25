# Day 12 -- Breather & Revision (Days 01--11)

## 📌 Goal

Consolidate Linux fundamentals learned from Days 01--11 and reinforce
core concepts through light hands-on revision.

------------------------------------------------------------------------

# ✅ Mindset & Plan Review (Day 01)

-   Original Goal: Build strong Linux foundation for DevOps.
-   Status: On track.
-   Adjustments:
    -   Practice permissions (`chmod`, `chown`) more deeply.
    -   Improve service troubleshooting confidence.
-   Key Realization: Consistency \> Motivation.

------------------------------------------------------------------------

# 🔄 Processes & Services Revision (Day 04 & 05)

## Commands Re-run

ps aux \| head systemctl status ssh journalctl -u ssh -n 20

## Observations

-   `ps aux` → Lists running processes with PID, CPU, memory usage.
-   `systemctl status` → Shows if service is active, failed, or
    inactive.
-   `journalctl -u` → Displays service logs for troubleshooting.

💡 Service debugging flow = Status → Logs → Process check

------------------------------------------------------------------------

# 📂 File Skills Practice (Days 06--11)

## Commands Practiced

echo "Revision entry" \>\> revision.txt chmod 755 revision.txt ls -l
revision.txt mkdir practice-dir cp revision.txt practice-dir/

## Ownership Practice

sudo chown tokyo revision.txt sudo chgrp heist-team revision.txt ls -l
revision.txt

## What I Reinforced

-   `>>` appends safely without overwriting.
-   `755` = rwxr-xr-x
-   `ls -l` verifies permissions & ownership.
-   Ownership changes require `sudo`.

------------------------------------------------------------------------

# 🚨 Top 5 Commands for Incidents

1.  `ls -l`
2.  `ps aux`
3.  `systemctl status <service>`
4.  `journalctl -xe`
5.  `df -h`

------------------------------------------------------------------------

# 👥 User & Group Sanity Check

## Scenario Practiced

sudo useradd demo-user sudo groupadd demo-group sudo chown
demo-user:demo-group revision.txt id demo-user ls -l revision.txt

## Verification

-   `id` confirms UID & group membership.
-   `ls -l` confirms ownership change.

------------------------------------------------------------------------

# 🧠 Mini Self-Check

## 1) Which 3 commands save the most time?

-   `ls -l`
-   `systemctl status`
-   `ps aux`

## 2) How to check if a service is healthy?

systemctl status nginx journalctl -u nginx -n 50 ps aux \| grep nginx

## 3) How to safely change ownership & permissions?

sudo chown -R appuser:appgroup /var/www/app sudo chmod -R 755
/var/www/app

Best Practice: - Verify user & group exist. - Avoid using `777`. -
Always re-check with `ls -l`.

## 4) Focus for Next 3 Days

-   Master numeric permissions.
-   Improve log filtering skills.
-   Practice real-world troubleshooting scenarios.

------------------------------------------------------------------------

# 🎯 Key Takeaways

-   Always verify after making changes.
-   Permissions control system security.
-   Logs are critical for troubleshooting.
-   Ownership is essential in deployments.
-   Daily practice builds operational confidence.
