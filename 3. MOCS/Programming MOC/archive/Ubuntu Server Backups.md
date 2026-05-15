---
type: Programming Note
programming language:
related:
completed: false
created: 2026-05-14T19:22
updated: 2026-05-14T19:23
---
## Introduction

I already use zfs to create a software mirror between my drives, but I want to follow the The 3-2-1 Rule.

We want 3 copies of the data, on 2 different media types, with 1 off-site.
- **Copy 1:** The live instance (RAID 1)
- **Copy 2:** A External SSD (Local, fast recovery)
- **Copy 3:** Cloud Drive (Off-site, disaster recovery)
  
For now I will use my google drive as the off-site, backup in the future the ideal setup would be to have a secondary server/nas to a friend/family house, to save the off site backup to.

Its important to use an ssd as secondary local backup, this because hardisk risk to be dameged in harquakes, but ssd do not.

## Software Installation

To do this we will need to install some software:

```bash
sudo apt update
sudo apt install borgbackup borgmatic rclone
```

- **BorgBackup (Borg):** It handles deduplication (only saves changes), compression, and encryption. It turns your files into a secure, efficient "repository."
- **Borgmatic:** The "Manager." It’s a wrapper that allows you to configure everything in a simple `.yaml` file.
- **Rclone:** It specializes in moving files between your local system and cloud providers like Google Drive.

## SSD Permanent Mounting

**Step 1: Find SSD by-id the ID**

Plug in your SSD and run:

```bash
ls -l /dev/disk/by-id/
```

Look for a name that represents your drive (e.g., `ata-Samsung_SSD_870_EVO_S6P...` or `usb-External_Drive_...`). You want the one for the **partition** (usually ending in `-part1`).

In my case in the output there were a lot of line but the one that got my attention where these:

```text
lrwxrwxrwx 1 root root 9 May 13 17:30 usb-Realtek_RTL9210_NVME_012345678904-0:0 -> ../../sdd
lrwxrwxrwx 1 root root 10 May 13 17:30 usb-Realtek_RTL9210_NVME_012345678904-0:0-part1 -> ../../sdd1
```

So in my case the ***by-id*** of the ssd is `usb-Realtek_RTL9210_NVME_012345678904-0:0-part1`.

>[!note] by-id
>
>We use **`by-id`** because unlike a `UUID` (which changes if you reformat the drive) or `/dev/sdb` (which changes if you plug it into a different port), the `by-id` is tied to the **physical serial number** of the SSD.

**Step 2: Wipe and Format the external SSD**

We will format the SSD we will call it `backup_ssd` and we will use the `ext4` filesystem since is the one preferred by `borg` (the backup software that we will use).

```bash
# WARNING: This erases everything on the SSD!
sudo mkfs.ext4 /dev/disk/by-id/usb-Realtek_RTL9210_NVME_012345678904-0:0-part1
```

**Step 3: Create the Mount Point**

```bash
sudo mkdir -p /mnt/backup_ssd
```

**Step 4: Edit /etc/fstab**

Open the file `sudo vim /etc/fstab` and add this line at the bottom:

```text
/dev/disk/by-id/usb-YOUR_DRIVE_ID-part1  /mnt/backup_ssd  ext4  defaults,nofail,noatime  0  2
```

>[!warning] Notes
>- `nofail`: This is the most important part. It tells Ubuntu: "If the SSD is unplugged at boot, don't freeze the whole server; just keep going."
>- `noatime`: Reduces wear on your SSD by not writing "last accessed" timestamps every time a file is read.
>- The first digit (`0`): This is for **Dump**. It’s a very old backup utility. Almost no one uses it anymore, so we set it to `0` (disabled).
>- The second digit (`2`): This is for **fsck** (File System Check). It tells Ubuntu whether to check the drive for errors during a reboot:
>	- `0`: Never check. (Risky for backup drives).
>	- `1`: Check first (Reserved for your OS/Root drive).
>	- `2`: Check later. This is perfect for external drives. It means if the server loses power, Ubuntu will quickly scan the SSD for errors during the next boot _after_ the main system is up.

**Step 5: Mount & Test**

Normally the drives are mounted at boot, but to tell the oss to remount all the drives we can use:
- `sudo systemctl daemon-reload` to be sure that the modification we did to `/etc/fstab` are applied
- `sudo mount -a` to remount all the drives (including the recently added external ssd)

**Step 6: add non root user ownership**

Once it is mounted via `/etc/fstab`, the drive will likely be owned by `root`. Since your Immich/Docker setup might need access, or you might want to run backups as a specific user, you should take ownership of the mount point after mounting it:

```bash
sudo chown $USER:$USER /mnt/backup_ssd
```

## Borg Repository

**Step 1: Borg repository initialization**

Initialize your repository on the SSD using this command:

```bash
borg init --encryption=repokey /mnt/backup_ssd/borg_backup
```

***Replace:***
- `/mnt/backup_ssd/borg_backup` with the path where you want to create the repo, in particular replace `/mnt/backup_ssd` with the path to where you mounted your ssd.

***Password:*** After running it it will ask you to paste a password, do not lose it, (i used bitwarden to generate and save the password)

**Step 2: export repository key**

It's a good roule to export and save you repokey that borg automatically generates

Use this command to print the key on the terminal:

```bash
borg key export /mnt/backup_ssd/borg_backup
```
  
Copy it and save it somewhere save, i printed it on a sheet of paper and also saved it in bitwarden.
  
**Step 3: Create the Backup automation**

Let's create a the automation file for borgmatic, with these commands:

```bash
sudo mkdir -p /etc/borgmatic.d
sudo vim /etc/borgmatic.d/immich.yaml
```
  
  And write this:

```yaml
location:
    source_directories:
        - /home/rima/data/docker/immich
    
    repositories:
        - /mnt/backup_ssd/borg_backup

    exclude_patterns:
        - '**/thumbs'
        - '**/encoded-video'
        - '**/postgres_data'

storage:
    encryption_passphrase: "ln6kG#j%jV#0ilUO"
    compression: lz4

retention:
    keep_daily: 7
    keep_weekly: 4
    keep_monthly: 6

hooks:
    before_backup:
        - echo "Creating directory for DB dump if it doesn't exist..."
        - mkdir -p /home/rima/data/docker/immich/database-backup
        - echo "Dumping database..."
        - docker exec -t immich_postgres pg_dumpall --clean --if-exists -U postgres > /home/rima/data/docker/immich/database-backup/immich-database.sql
    
    after_backup:
        - rm /home/rima/data/docker/immich/database-backup/immich-database.sql
        - echo "Local backup complete. Syncing to Google Drive..."
        - rclone sync -P /mnt/backup_ssd/borg_backup gdrive:Backups/immich
        - echo "All backups finished successfully!"
```

**Replace:**
- `[PATH_TO_YOUR_IMMICH_DIRECTORY]` with your path to the immich directory in my case it is `/home/rima/data/docker/immich`
- `"YourSecurePasswordHere"` with a real secure password, mine is saved on bitwarden
  
  
**Step 4: Test Run**

The backup is automatically executed daily, to se the next is scheduled you can use:

```bash
systemctl list-timers borgmatic.timer
```

But since we never tested it we can force it to run the backup by using:

```bash
sudo borgmatic create --verbosity 1 --list --stats
```

This will tell if there are any errors, note that probably that the `rclone sync -P /mnt/backup_ssd/borg_backup gdrive:Backups/immich` command will fail, since we still have to configure it.

## Rclone Google Drive Encrypted Backup

>[!danger] The "Root" Trap (Crucial First Step)
>
>Because Borgmatic runs as the `root` user (via `sudo`), it will only look for cloud credentials belonging to `root`. If you set this up as your normal user (`rima`), Borgmatic will fail to connect.
>
>You **must** start the configuration with `sudo`.

**Step 1: Get Your Personal Google Client ID**

You need to generate these credentials from Google.

1. Go to the **[Google Cloud Console](https://console.cloud.google.com/)** and log in with your Google account.
2. *Create a New Project:* Click the project dropdown at the top and select "New Project" (name it something like `rclone-backup`).
3. *Enable the API:* Go to "APIs & Services" > "Library". Search for `Google Drive API` and click `Enable`.
4. *OAuth Consent Screen:* Go to "APIs & Services" > "OAuth consent screen".
    - Choose `External` and click Create.
    - Fill in the required fields (App name: `rclone`, User support email: `your email`, Developer contact: `your email`). You can skip the rest and just click "Save and Continue" through the other screens.
    - On the summary screen, click `Publish App` (so the token doesn't expire in 7 days).
5. *Create Credentials:*
    - Go to "APIs & Services" > "Credentials".
    - Click `+ CREATE CREDENTIALS` > `OAuth client ID`.
    - Application type: `Desktop app`.
    - Name: `rclone`.
    - Click `Create`.
6. *Save your Keys:* It will pop up a window with your `Client ID` and `Client Secret`, save  them or simply leave this window open, since they will be needed for the next step.

**Step 2: Start the Rclone Configurator**

Run this command on your server:

```bash
sudo rclone config
```

**Step 3: The Setup Wizard**

Rclone will ask you a series of questions. Here is exactly how to answer them to match the `gdrive:Backups/immich` path we put in the borg YAML file:

1. *e/n/d/r/c/s/q>* Type `n` (New remote).
2. *name>* Type `gdrive` (This must match exactly what we put in the yaml!).
3. *Storage>* Scroll through the list and find `Google Drive`. Type the number next to it (usually it's `18`, `17`, or just type `drive`).
4. *client_id>* Paste the `Client ID` created at the **step 1**.
5. *client_secret>* Paste the `Client Secret` created at the **step 1**.
6. *scope>* Type `1` (Full access, needed to create folders and upload files).
7. *service_account_file>* Leave blank and press `Enter`.
8. *Edit advanced config?* Type `n` (No).
9. *Use auto config?* 
	- If you are doing this on a monitor connected directly to the server with a web browser, type `y`.
	- If you are connected via SSH, type `n`.

**Step 4: Authorizing Google Drive (Headless SSH)**

If you typed `n` for auto-config, `rclone` will give you a command that looks something like this: `rclone authorize "drive" "eyJzY29wZ... "`
1. You need to copy that exact command and run it in the terminal/command prompt of your **local personal computer** (the laptop/desktop you are using right now, which has a web browser). _Note: You'll need to download the rclone executable to your personal PC for this one step._
2. It will open your web browser, ask you to log into Google, and grant permission.
3. Your local terminal will then spit out a long code (a token).
4. Copy that token, go back to your server's SSH session, and paste it in.

**Step 5: Finalize**
1. *Configure this as a Shared Drive (Team Drive)?* Type `n` (No).
2. It will show you a summary. Type `y` to confirm.
3. Type `q` to quit the configurator.

**Step 5: Test the Connection**

Let's make sure your server can actually talk to your Google Drive. Run this:

```Bash
sudo rclone mkdir gdrive:Backups/immich
sudo rclone ls gdrive:Backups
```

## Final Run

The backup is automatically executed daily, but to test it we can force by using:

```bash
sudo borgmatic create --verbosity 1 --list --stats
```
