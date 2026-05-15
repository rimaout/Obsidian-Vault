---
type: Programming Note
programming language:
related:
completed: false
created: 2026-05-14T19:24
updated: 2026-05-15T18:44
---
## Introduction

To have the piace of mind that the drives will not die without me knowing we will use smartmontools and zfs tools to test the healt of my drives and then we will use telegram to get notification on drives health.

There will be 3 types of tests:
- A daily test that ...
- A weekly tests that ...
- A monthly tests that ...

## Install Software

```bash
sudo apt update 
sudo apt install smartmontools curl -y
```

## Create the Telegram Bot

1. **Open Telegram** and search for `@BotFather`.
2. Send `/newbot`. Follow the prompts to name it.
3. **Save the API Token** it gives you (e.g., `123456:ABC-DEF...`).
4. **Get your Chat ID:**
    - Message your new bot directly to activate a chat (send "Hi").
    - In your browser, go to: `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates`
    - Look for `"id":` inside the `"chat":` block. That is your **Chat ID**.

## Daily Drives Health Check

This script checks the physical health of every drive and the logical health of your ZFS pool.

**Create the file:**

```bash
sudo vim /usr/local/bin/check_disks_telegram.sh
```

**Paste this content:**

>[!danger] Replace with your real data
>
>Replace:
>- `TOKEN` with your bot token (generated at [[#Create the Telegram Bot]])
>- `CHAT_ID` with your chat id (generated at [[#Create the Telegram Bot]])
>- `POOL` with your zfs pool (in my case is named `tank`, to see yous you can use the command `zpool list`)

```bash
#!/bin/bash

# --- CONFIGURATION ---
TOKEN="YOUR_REDACTED_TOKEN"
CHAT_ID="YOUR_REDACTED_ID"

TEMP_THRESHOLD=45
REPORT_DAY="01" 

DISKS=$(lsblk -dno NAME,TYPE | grep disk | awk '{print "/dev/"$1}')

send_telegram() {
    curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" \
    --data-urlencode "chat_id=$CHAT_ID" \
    --data-urlencode "parse_mode=HTML" \
    --data-urlencode "text=$1"
}

ERROR_COUNT=0
HEALTH_REPORT="🔍 <b>Disk Health Report: $(hostname)</b>"$'\n\n'

# 1. Build the Main Summary Report
for DISK in $DISKS; do
    STATUS=$(sudo smartctl -H "$DISK" | grep -iE "result|health" | awk -F': ' '{print $NF}' | xargs)
    TEMP=$(sudo smartctl -a "$DISK" | awk '/^194 / {print $10; exit} /^Temperature:/ {print $2; exit} /Current Drive Temperature:/ {print $4; exit}')
    SCARY_METRICS=$(sudo smartctl -A "$DISK" | grep -E 'Reallocated_Sector|Current_Pending_Sector|Offline_Uncorrectable' | awk '$10 > 0 {print $2": "$10}')

    RE_NUM='^[0-9]+$'
    if ! [[ $TEMP =~ $RE_NUM ]] ; then
        TEMP_DISPLAY="??"
        TEMP_VAL=0
    else
        TEMP_DISPLAY="$TEMP"
        TEMP_VAL=$TEMP
    fi

    # Format output based on health
    if [[ "$STATUS" =~ (FAIL|DEGRADE) ]] || [ ! -z "$SCARY_METRICS" ] || [ "$TEMP_VAL" -gt "$TEMP_THRESHOLD" ]; then
        HEALTH_REPORT+="🚨 <b>ALERT: $DISK</b>"$'\n'
        HEALTH_REPORT+="   - Status: ${STATUS:-UNKNOWN}"$'\n'
        HEALTH_REPORT+="   - Temp: ${TEMP_DISPLAY}°C"$'\n'
        [ ! -z "$SCARY_METRICS" ] && HEALTH_REPORT+="   - Issues: $SCARY_METRICS"$'\n'
        HEALTH_REPORT+=$'\n'
        ((ERROR_COUNT++))
    else
        HEALTH_REPORT+="✅ <b>HEALTHY: $DISK</b>"$'\n'
        HEALTH_REPORT+="   - Status: ${STATUS:-PASSED}"$'\n'
        HEALTH_REPORT+="   - Temp: ${TEMP_DISPLAY}°C"$'\n\n'
    fi
done

# ZFS Check
ZFS_STATUS=$(zpool status -x)
if ! echo "$ZFS_STATUS" | grep -q "all pools are healthy"; then
    HEALTH_REPORT+="🚨 <b>ZFS WARNING:</b> Some pools are not healthy!"$'\n'
    ((ERROR_COUNT++))
fi

# 2. Send the Main Summary Message
if [ "$ERROR_COUNT" -gt 0 ]; then
    send_telegram "‼️ <b>URGENT DISK ALERT</b> ‼️"$'\n\n'"$HEALTH_REPORT"
elif [ "$(date +%d)" == "$REPORT_DAY" ]; then
    send_telegram "📅 <b>Monthly Detailed Health Check-in</b>"$'\n\n'"$HEALTH_REPORT"
fi

# 3. Send Individual Detailed Logs (Only on Report Day)
if [ "$(date +%d)" == "$REPORT_DAY" ]; then
    for DISK in $DISKS; do
        # Use -x for maximum detail
        RAW_SMART=$(sudo smartctl -x "$DISK")
        ESCAPED_SMART=$(echo "$RAW_SMART" | sed 's/&/\&amp;/g; s/</\&lt;/g; s/>/\&gt;/g')
        
        # Enforce Telegram's 4096 character limit
        if [ ${#ESCAPED_SMART} -gt 3800 ]; then
            FINAL_SMART="${ESCAPED_SMART:0:3800}"$'\n\n... [LOG TRUNCATED DUE TO TELEGRAM LENGTH LIMIT] ...'
        else
            FINAL_SMART="$ESCAPED_SMART"
        fi

        DRIVE_LOG_MSG="<b>$DISK Detailed Log:</b>"$'\n'
        DRIVE_LOG_MSG+="<blockquote expandable><code>$FINAL_SMART</code></blockquote>"
        
        send_telegram "$DRIVE_LOG_MSG"
        
        # Small delay so Telegram doesn't rate-limit our bot
        sleep 1 
    done
fi
```

**Make it executable:**

```bash
sudo chmod +x /usr/local/bin/check_disks_telegram.sh
```

### Daily Systemd Timer

To run this daily we use a `Systemd Timer` this is a create solution because even if the timer is skipped because the server was of the Systemd timer is smart enouft to run it if it skipped it

**Step 1: Create the service

```bash
sudo vim /etc/systemd/system/disk-health.service
```

Paste this:

```TOML
[Unit]
Description=Daily Disk Health Check for Telegram
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/check_disks_telegram.sh

# Add a retry in case of temporary DNS/Network blips
Restart=on-failure
RestartSec=30s
```

**Step 2: Create the Timer

```bash
sudo vim /etc/systemd/system/disk-health.timer
```

Paste this:

```TOML
[Unit]
Description=Run Disk Health Check Daily and catch up if missed

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

**Step 3: Activate Timer**

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now disk-health.timer
```

**Step 4: Test Run**

To make sure everything is working right now, you can manually trigger the service:

```bash
sudo systemctl start disk-health.service
```

Since it may not be the 1st of the month, the script will only send a Telegram message **if it finds a disk error**. If you want to test the Telegram connection right now regardless of errors, you can temporarily change the script line `if [ "$DAY" == "01" ];` to the current day of the month.

## Weekly Short Drivers Test

**Create the file:**

```bash
sudo vim /usr/local/bin/weekly_disk_test.sh
```

**Paste this:**

```bash
#!/bin/bash

# --- CONFIGURATION ---
TOKEN="YOUR_BOT_TOKEN"
CHAT_ID="YOUR_CHAT_ID"

DISKS=$(lsblk -dno NAME,TYPE | grep disk | awk '{print "/dev/"$1}')

send_telegram() {
    # Changed parse_mode to HTML to support expandable sections
    curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" \
    --data-urlencode "chat_id=$CHAT_ID" \
    --data-urlencode "parse_mode=HTML" \
    --data-urlencode "text=$1"
}

# 1. Notify that we are starting
START_MSG="🛠️ <b>Weekly Short SMART Tests Started: $(hostname)</b>"$'\n'"Please wait ~3 minutes for results..."
send_telegram "$START_MSG"

# 2. Trigger tests on all disks
for DISK in $DISKS; do
    sudo smartctl -t short "$DISK" > /dev/null
done

# 3. Wait for tests to finish
# Short tests reliably take 2 minutes. We wait 3 minutes (180 seconds) to be safe.
sleep 180

# 4. Gather Results
REPORT="📊 <b>Weekly Short Test Results:</b>"$'\n\n'
RAW_DETAILS=""
ERROR_COUNT=0

for DISK in $DISKS; do
    # Extract the entire result line instead of specific columns
    TEST_RESULT=$(sudo smartctl -l selftest "$DISK" | grep "^# 1")
    
    # Fallback if the drive doesn't report properly (e.g., NVMe or USB drives)
    if [ -z "$TEST_RESULT" ]; then
         # Check basic health as a fallback for NVMe
         HEALTH_CHECK=$(sudo smartctl -H "$DISK" | grep -i "passed")
         if [ ! -z "$HEALTH_CHECK" ]; then
             TEST_RESULT="Completed without error (Health OK fallback)"
         else
             TEST_RESULT="Status Unknown (Check manually)"
         fi
    fi
    
    # Evaluate the result (Clean Summary)
    if [[ "$TEST_RESULT" == *"Completed"* ]]; then
         REPORT+="✅ $DISK: Completed without error"$'\n'
    else
         REPORT+="⚠️ $DISK: $TEST_RESULT"$'\n'
         ((ERROR_COUNT++))
    fi
    
    # Save the raw output for the collapsible section
    RAW_DETAILS+="<b>$DISK:</b>"$'\n'"<code>${TEST_RESULT}</code>"$'\n\n'
done

# Attach the raw details as an expandable blockquote (collapsible section)
REPORT+=$'\n'"<blockquote expandable><b>Raw Logs:</b>"$'\n'"$RAW_DETAILS</blockquote>"

# 5. Send Final Report
if [ "$ERROR_COUNT" -gt 0 ]; then
    send_telegram "🚨 <b>WARNING: WEEKLY TEST FAILED</b> 🚨"$'\n\n'"$REPORT"
else
    send_telegram "$REPORT"
fi
```

**Make it executable:** 

```bash
sudo chmod +x /usr/local/bin/weekly_disk_test.sh
```

### Weekly Timer


**Step 1: Create the service

```bash
sudo vim /etc/systemd/system/weekly-disk-test.service
```

Paste this:

```TOML
[Unit]
Description=Weekly Short Disk Health Check for Telegram
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/weekly_disk_test.sh

# Add a retry in case of temporary network drops
Restart=on-failure
RestartSec=30s
```

**Step 2: Create the timer

```bash
sudo vim /etc/systemd/system/weekly-disk-test.timer
```

Paste this:

```TOML
[Unit]
Description=Run Disk Health Check Weekly (Sundays at 4 AM)

[Timer]
# Runs every Sunday at 04:00 AM
OnCalendar=Sun *-*-* 04:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

**Step 3: Activate Timer**

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now weekly-disk-test.timer
```

**Step 4: Test Timer**

To make sure everything is working right now, you can manually trigger the service:

```bash
sudo systemctl start weekly-disk-test.service
```

## Monthly Long Drive Test

**Create the file:**

```bash
sudo vim /usr/local/bin/monthly_long_test.sh
```

**Paste this:**

```bash
#!/bin/bash

# --- CONFIGURATION ---
TOKEN="YOUR_BOT_TOKEN"
CHAT_ID="YOUR_CHAT_ID"

DISKS=$(lsblk -dno NAME,TYPE | grep disk | awk '{print "/dev/"$1}')

send_telegram() {
    curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" \
    --data-urlencode "chat_id=$CHAT_ID" \
    --data-urlencode "parse_mode=HTML" \
    --data-urlencode "text=$1"
}

# 1. Notify Start
send_telegram "🏗️ <b>Monthly SMART Long Tests Started: $(hostname)</b>"$'\n'"This scan checks every sector. Results in ~12 hours."

# 2. Trigger Long Tests
for DISK in $DISKS; do
    sudo smartctl -t long "$DISK" > /dev/null
done

# 3. Wait for tests (Long tests can take 10+ hours, we wait 12)
sleep 12h

# 4. Gather Results
REPORT="🔭 <b>Monthly Long Test Results:</b>"$'\n\n'
RAW_DETAILS=""
ERROR_COUNT=0

for DISK in $DISKS; do
    TEST_RESULT=$(sudo smartctl -l selftest "$DISK" | grep "^# 1")
    
    if [ -z "$TEST_RESULT" ]; then
         HEALTH_CHECK=$(sudo smartctl -H "$DISK" | grep -iE "passed|ok")
         if [ ! -z "$HEALTH_CHECK" ]; then
             TEST_RESULT="Completed without error (Health OK fallback)"
         else
             TEST_RESULT="Status Unknown (Check manually)"
         fi
    fi
    
    if [[ "$TEST_RESULT" == *"Completed"* ]]; then
         REPORT+="✅ $DISK: Passed"$'\n'
    else
         REPORT+="🚨 $DISK: FAILED"$'\n'
         ((ERROR_COUNT++))
    fi
    
    ESCAPED_RESULT=$(echo "$TEST_RESULT" | sed 's/&/\&amp;/g; s/</\&lt;/g; s/>/\&gt;/g')
    RAW_DETAILS+="<b>$DISK:</b>"$'\n'"<code>${ESCAPED_RESULT}</code>"$'\n\n'
done

REPORT+=$'\n'"<blockquote expandable><b>Detailed SMART Logs:</b>"$'\n'"$RAW_DETAILS</blockquote>"

if [ "$ERROR_COUNT" -gt 0 ]; then
    send_telegram "‼️ <b>CRITICAL: LONG TEST FAILURES</b> ‼️"$'\n\n'"$REPORT"
else
    send_telegram "$REPORT"
fi
```

**Make it executable:** 

```bash
sudo chmod +x /usr/local/bin/monthly_long_test.sh
```

### Monthly Timer


**Step 1: Create the service

```bash
sudo vim /etc/systemd/system/monthly-long-test.service
```

Paste this:

```TOML
[Unit]
Description=Monthly SMART Long Disk Health Check for Telegram
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/monthly_long_test.sh

# Add a retry in case of temporary network drops
Restart=on-failure
RestartSec=30s
```

**Step 2: Create the timer

```bash
sudo vim /etc/systemd/system/monthly-long-test.timer
```

Paste this:

```TOML
[Unit]
Description=Run SMART Long Test Monthly (1st of the month at 2 AM)

[Timer]
# Runs on the 1st day of every month at 02:00:00
OnCalendar=*-*-01 02:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

**Step 3: Activate Timer**

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now monthly-long-test.timer
```

**Step 4: Test Timer**

To make sure everything is working right now, you can manually trigger the service:

You can manually trigger the service right now to verify the script and Telegram notifications are working. Note that because of the `sleep 12h` in the script, this command will appear to "hang" in your terminal until the test window is over, or you can check your Telegram for the start notification.

```bash
sudo systemctl start monthly-long-test.service
```

## Monthly  ZFS Scrub

```bash
sudo vim /usr/local/bin/monthly_zfs_scrub.sh
```

Paste this:

```bash
#!/bin/bash

# --- CONFIGURATION ---
TOKEN="YOUR_BOT_TOKEN"
CHAT_ID="YOUR_CHAT_ID"
POOL="tank" # Change this to your pool name

send_telegram() {
    curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" \
    --data-urlencode "chat_id=$CHAT_ID" \
    --data-urlencode "parse_mode=HTML" \
    --data-urlencode "text=$1"
}

# 1. Notify Start
send_telegram "🧹 <b>Monthly ZFS Scrub Started: $(hostname)</b>"$'\n'"Verifying data checksums on pool: <b>$POOL</b>"

# 2. Trigger Scrub and Wait for it to finish
sudo zpool scrub "$POOL"
sudo zpool wait "$POOL"

# 3. Gather Results
SCRUB_STATUS=$(zpool status "$POOL")
# Check if there are any errors in the status
if echo "$SCRUB_STATUS" | grep -qi "errors: No known data errors"; then
    RESULT_ICON="✅"
    SUMMARY="Scrub completed: No errors found."
else
    RESULT_ICON="🚨"
    SUMMARY="Scrub completed: ERRORS DETECTED!"
    ERROR_FLAG=true
fi

# Format the report
REPORT="$RESULT_ICON <b>ZFS Scrub Results:</b>"$'\n'"$SUMMARY"$'\n\n'

# Escape ZFS output for the raw log section
ESCAPED_STATUS=$(echo "$SCRUB_STATUS" | sed 's/&/\&amp;/g; s/</\&lt;/g; s/>/\&gt;/g')
REPORT+="<blockquote expandable><b>Full ZFS Status:</b>"$'\n'"<code>$ESCAPED_STATUS</code></blockquote>"

# 4. Send Report
if [ "$ERROR_FLAG" = true ]; then
    send_telegram "‼️ <b>URGENT: ZFS DATA CORRUPTION</b> ‼️"$'\n\n'"$REPORT"
else
    send_telegram "$REPORT"
fi
```


**Make it executable:** 

```bash
sudo chmod +x /usr/local/bin/monthly_zfs_scrub.sh
```

### Monthly Timer

**Step 1: Create the Service**

Create the service file for the ZFS scrub operation.

```bash
sudo vim /etc/systemd/system/monthly-zfs-scrub.service
```

Paste the following:

```TOML
[Unit]
Description=Monthly ZFS Scrub for Telegram
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/monthly_zfs_scrub.sh
# Add a retry in case of temporary network drops
Restart=on-failure
RestartSec=30s
```

**Step 2: Create the Timer**

Create the timer file to schedule the scrub for mid-month.

```bash
sudo vim /etc/systemd/system/monthly-zfs-scrub.timer
```

Paste the following:

```TOML
[Unit]
Description=Run ZFS Scrub Monthly (15th of the month at 2 AM)

[Timer]
# Runs on the 15th day of every month at 02:00:00
OnCalendar=*-*-15 02:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

**Step 3: Activate the Timer**

Reload the systemd daemon and enable the scrub timer.

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now monthly-zfs-scrub.timer
```

**Step 4: Test the Setup**

You can manually trigger the scrub service to verify the script. Because the script uses `zpool wait`, the command will stay active in your terminal until the scrub is completely finished. You will receive a Telegram message at the start and a detailed report once it completes.

```bash
sudo systemctl start monthly-zfs-scrub.service
```