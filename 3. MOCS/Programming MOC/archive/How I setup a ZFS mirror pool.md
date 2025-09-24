---
type: Programming Note
programming language:
related:
completed: false
created: 2025-09-22T13:17
updated: 2025-09-22T20:47
---
In my case I have to 3 drives in my pc:
1. one ssd with the os on (debian)
2. two hard disks, a 2tb and 1tb drives

My objective is to create a mirro using ZFS between the two hard disk for redundancy.  

### 1) Prep and safety

Since none of the two drives has already a ZFS file system, I will have to wipe everting on them a then create the ZFS partition

So first of all I made a backup of any important data on them (in my case the 2tb drive was already empty)

### 2) Identify disks
With the `lsblk` we can the disk and partition layout all the drives connecte: 

In my case the output is:

```
NAME                        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda                           8:0    0 223.6G  0 disk 
|-sda1                        8:1    0   976M  0 part /boot
|-sda2                        8:2    0     1K  0 part 
`-sda5                        8:5    0 222.6G  0 part 
  |-DebianServer--vg-root   254:0    0 211.3G  0 lvm  /
  `-DebianServer--vg-swap_1 254:1    0  11.3G  0 lvm  [SWAP]
sdb                           8:16   0   1.8T  0 disk 
sdc                           8:32   0 931.5G  0 disk 
`-sdc1                        8:33   0 931.5G  0 part 
```

- `sda` is the ssd with the debian os partition
- `sdb` is the 2tb empty drive
- `sdc` is the 1tb drive, but it has a `sdc1` partition with some data one 

### 3) Clean disk partition tables (remove sdc1)

Since `sdc1` is not a ZFS partition I have to remove it, so after copy all the that in a external drive:

1. Unmount partition if mounted: `sudo umount /dev/sdc1 || true`
2. Wipe signatures and partition table:
	```bash
	sudo wipefs -a /dev/sdc  
	```
  
>[!note]- Notes
>- wipefs removes filesystem signatures; sgdisk --zap-all clears the GPT/MBR. Both will erase existing data.
>- GPT (GUID Partition Table) and MBR (Master Boot Record) are partition table schemes that define how disk partitioning and boot information are stored.

### 4) Check sector sizes (to pick ashift)

Before creating the ZFS pool we have to see what's the physical sector size of the drives (sdb, sdc): 

```bash
sudo cat /sys/block/sdb/queue/physical_block_size  
sudo cat /sys/block/sdc/queue/physical_block_size
```

Output:
```
4096
4096
```

So I will use the `ashift=12` flag when creating the ZFS pool to match 4096B physical sectors.

>[!note]- Notes
>
>I did't understand why was this important so I asked, to chat why is important to use `ashift=12`.
>
>***Short answer:*** matching ashift to the physical sector size (4096 → ashift=12) ensures ZFS writes are aligned to the drive’s native erase/write unit, preventing extra read‑modify‑write cycles, larger write amplification, reduced performance, and wasted space. If you set ashift too small (ashift=9 for 512 bytes) on a 4K physical drive you’ll see worse throughput and more wear; if you set it larger than needed you lose some usable space but avoid the performance penalty.

### 5) Use stable by-id paths

Instead of using `sdb`, `sdc` names to refer to the drives when creating the pool, is better to use by-id identifiers.

To get the by-id identifiers of `sdb` I did `ls -l /dev/disk/by-id | egrep "$(basename /dev/sdb)"`, the output was:

```
lrwxrwxrwx 1 root root 9 Sep 22 11:09 ata-ST2000DM008-2FR102_WFL3W1K2 -> ../../sdb
lrwxrwxrwx 1 root root 9 Sep 22 11:09 wwn-0x5000c500cfb22756 -> ../../sdb
``` 

So when we will create the pool I'll use use `/dev/disk/by-id/wwn-0x5000c500cfb22756` instead of `/dev/sdb`.

An I repeated the same thing for `sdc`,  so I did `ls -l /dev/disk/by-id | egrep "$(basename /dev/sdc)"`, the output was:

```
lrwxrwxrwx 1 root root 9 Sep 22 11:09 ata-WDC_WD10EZEX-00WN4A0_WD-WCC6Y1RPEPX8 -> ../../sdc
lrwxrwxrwx 1 root root 9 Sep 22 11:09 wwn-0x50014ee20d218f51 -> ../../sdc
```

So when we will create the pool I'll use use `/dev/disk/by-id/wwn-0x50014ee20d218f51` instead of `/dev/sdb`.

>[!note]- Notes
>- `/dev/sdX` names can change across reboots or when devices are added/removed.
>- `/dev/disk/by-id` entries are stable and uniquely identify the physical disk (use wwn-... or ata-...).

### 6) Create the ZFS mirror pool

Using all the information I gathered we can create the mirror betwen the two disk using this coomand:

```bash
sudo zpool create -f -o ashift=12 tank mirror /dev/disk/by-id/wwn-0x5000c500cfb22756 /dev/disk/by-id/wwn-0x50014ee20d218f51
```

Explanation of options:
- `create`: build a new ZFS pool.
- `-f`: force (overwrites existing metadata on disks).
- `-o ashift=12`: set allocation block size to 2^12 = 4096 bytes.
- `tank`: pool name (change if you prefer).
- `mirror /dev/... /dev/...`: create a mirror vdev across the two specified disks.

>[!note] Verify Pool Status
>```
>sudo zpool status -v
>sudo zpool list
>```

### 8) Recommended pool/dataset settings

- Enable compression: `sudo zfs set compression=lz4 tank`
- Disable atime updates: `sudo zfs set atime=off tank`
  
>[!note]- Notes
>
>This were to setting that many people i foud suggesting online, for what I understood:
> - `compression=lz4` transparently compresses data so it saves disk space and often improves throughput for compressible data with low CPU cost.
> - `atime=off` prevents updating file access time on every read. Reduces the wear and improves performance (good for most workloads). Downside: last-access timestamps won’t be accurate.
>   
>Disabling `atime` update can cause problem for certain workloads, but in my case for a home server shoud not create any problem

### 9) Create datasets and mountpoints
- Example:
  sudo zfs create -o mountpoint=/tank/data tank/data
- Notes:
  - Datasets are lightweight filesystems inside the pool. You can set individual properties (compression, atime) per dataset.
  - mountpoint sets where the dataset is mounted in your filesystem (change /tank/data as desired).

Verify mounts and usage:
- sudo zfs list  
- df -h /tank

### 10) Services and boot behavior
- Ensure ZFS services enable auto-import/mount at boot:
  sudo systemctl enable --now zfs-import-cache zfs-mount zfs.target

Why: zfs-import-cache imports pools at boot. zfs-mount mounts datasets. Enabling ensures your pool is available automatically.

### 11) Maintenance tasks
- Regular scrub (monthly recommended):
  sudo zpool scrub tank  
  Monitor: sudo zpool status -v
- Monitor pool health:
  sudo zpool status  
  sudo zpool list

### 12) Replacing/upgrading a mirrored disk later
- Typical workflow replacing the 1TB with a new 2TB:
  1) Optional: offline the old disk (if needed):
     sudo zpool offline tank /dev/disk/by-id/<old-by-id>
  2) Physically replace the disk.
  3) Replace in ZFS and start resilver:
     sudo zpool replace tank <old-by-id> /dev/disk/by-id/<new-by-id>
  4) Monitor resilver:
     sudo zpool status -v
  5) Expand to use full size (if pool doesn't auto-expand):
     sudo zpool online -e tank /dev/disk/by-id/<new-by-id>

Notes:
- ashift is set per vdev at creation and won’t change by replacing disks. To change ashift you must recreate the vdev/pool.  
- Use by-id names to avoid device-name confusion.

### 13) Quick reference commands
- Create pool:
  sudo zpool create -f -o ashift=12 tank mirror <by-id-for-sdb> <by-id-for-sdc>
- Status:
  sudo zpool status -v
- List pools:
  sudo zpool list
- Create dataset:
  sudo zfs create -o mountpoint=/tank/data tank/data
- Set compression/atime:
  sudo zfs set compression=lz4 tank  
  sudo zfs set atime=off tank
- Scrub:
  sudo zpool scrub tank

If you want this as a one-page printable checklist or automated scripts for scheduled scrubs, tell me which format you prefer.


Initial maintenance:
  sudo zpool scrub tank  
  sudo zpool status -v   # monitor scrub progress

>[!note] Note
>
>Reads all data, verifies checksums, and repairs errors using the mirror if a good copy exists. Run after creation and periodically (monthly is common).
