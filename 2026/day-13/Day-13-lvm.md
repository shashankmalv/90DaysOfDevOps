# Day 13 – Linux Volume Management (LVM)

## 🎯 Objective

Today I practiced Logical Volume Management (LVM) in Linux to understand how storage can be created, managed, and extended dynamically without repartitioning disks.

---

# 🔍 Step 1: Checked Current Storage

I first inspected the current disk and LVM state using:

```bash
lsblk
pvs
vgs
lvs
df -h
```

### What I Observed:
- No existing physical volumes (PV)
- No volume groups (VG)
- No logical volumes (LV)
- Standard system partitions were present

---

# 💽 Step 2: Created a Physical Volume (PV)

Since I didn’t have an extra disk, I created a virtual disk:

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a
```

Then initialized it as a Physical Volume:

```bash
pvcreate /dev/loop0
pvs
```

### Result:
- Physical volume created successfully
- Verified using `pvs`

---

# 📦 Step 3: Created a Volume Group (VG)

```bash
vgcreate devops-vg /dev/loop0
vgs
```

### Result:
- Volume group `devops-vg` created
- Free space available inside VG

---

# 📂 Step 4: Created a Logical Volume (LV)

```bash
lvcreate -L 4G -n app-data devops-vg
lvs
```

### Result:
- Logical volume `app-data` created with 4GB size
- Verified using `lvs`

---

# 🛠️ Step 5: Formatted and Mounted the Logical Volume

Formatted the LV:

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

Created mount directory and mounted it:

```bash
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h
```

Tested write access:

```bash
touch /mnt/app-data/testfile.txt
ls -l /mnt/app-data
```

### Result:
- Filesystem mounted successfully
- Able to create files inside mount point

---

# 📈 Step 6: Extended the Logical Volume

Extended the logical volume by 200MB:

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

Resized the filesystem:

```bash
resize2fs /dev/devops-vg/app-data
```

Verified the new size:

```bash
df -h /mnt/app-data
```

### Result:
- Logical volume increased from 4GB to 4.2GB
- Filesystem resized successfully
- New size reflected in `df -h`

---

# 🧠 Key Learnings

1. LVM provides flexible disk management without repartitioning.
2. Storage follows the hierarchy:
   - PV → VG → LV
3. After extending a logical volume, the filesystem must be resized.
4. LVM is very useful in production environments where storage needs to grow.
5. `lsblk`, `pvs`, `vgs`, `lvs`, and `df -h` are essential verification commands.

---

# 🧪 Commands Used

```bash
sudo -i

dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a

lsblk
pvs
vgs
lvs
df -h

pvcreate /dev/loop0
vgcreate devops-vg /dev/loop0
lvcreate -L 4G -n app-data devops-vg

mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data

lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h
```

---

# 🚀 Why LVM is Important for DevOps

- Allows dynamic storage scaling
- Prevents downtime during storage expansion
- Useful for databases and application servers
- Commonly used in cloud and enterprise environments

---

# ✅ Final Verification

```bash
lsblk
pvs
vgs
lvs
df -h
```

All components (PV, VG, LV) were successfully created, mounted, and extended.
