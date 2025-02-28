LVM (Logical Volume Management) is a **flexible and advanced disk management** system that allows resizing and managing disk storage dynamically.

---

## **Step 1: Install LVM (if not installed)**

For **Ubuntu/Debian**:

```bash
sudo apt install lvm2 -y

```

For **RHEL/CentOS**:

```bash
sudo yum install lvm2 -y

```

Enable and start the LVM service:

```bash
sudo systemctl enable lvm2-lvmetad
sudo systemctl start lvm2-lvmetad

```

---

## **Step 2: Check Available Disks**

List available disks and partitions:

```bash
lsblk

```

or

```bash
fdisk -l

```

---

## **Step 3: Create Physical Volumes (PVs)**

Identify the disks (`/dev/sdb`, `/dev/sdc`, etc.), then create PVs:

```bash
sudo pvcreate /dev/sdb /dev/sdc

```

Verify PV creation:

```bash
sudo pvdisplay

```

---

## **Step 4: Create a Volume Group (VG)**

Create a **volume group** named `vg_data` using PVs:

```bash
sudo vgcreate vg_data /dev/sdb /dev/sdc

```

Verify:

```bash
sudo vgdisplay

```

---

## **Step 5: Create a Logical Volume (LV)**

To create a **100GB** logical volume (`lv_storage`) inside `vg_data`:

```bash
sudo lvcreate -L 100G -n lv_storage vg_data

```

To use **all available space**:

```bash
sudo lvcreate -l 100%FREE -n lv_storage vg_data

```

Verify:

```bash
sudo lvdisplay

```

---

## **Step 6: Format the Logical Volume**

For **ext4** filesystem:

```bash
sudo mkfs.ext4 /dev/vg_data/lv_storage

```

For **XFS**:

```bash
sudo mkfs.xfs /dev/vg_data/lv_storage

```

---

## **Step 7: Mount the Logical Volume**

Create a mount point:

```bash
sudo mkdir /mnt/storage

```

Mount the volume:

```bash
sudo mount /dev/vg_data/lv_storage /mnt/storage

```

Verify:

```bash
df -h

```

---

## **Step 8: Permanent Mounting via `/etc/fstab`**

Find the **UUID**:

```bash
sudo blkid /dev/vg_data/lv_storage

```

Edit `/etc/fstab`:

```bash
sudo nano /etc/fstab

```

Add this line:

```
UUID=<your-uuid>  /mnt/storage  ext4  defaults  0  2

```

Save and apply:

```bash
sudo mount -a

```

---

## **Step 9: Extend a Logical Volume**

If you add a new disk and want to expand `lv_storage`:

```bash
sudo pvcreate /dev/sdd
sudo vgextend vg_data /dev/sdd
sudo lvextend -L +50G /dev/vg_data/lv_storage
sudo resize2fs /dev/vg_data/lv_storage  # (For ext4)

```

For **XFS**:

```bash
sudo xfs_growfs /mnt/storage

```

---

## **Step 10: Shrink a Logical Volume (Ext4 Only)**

**Unmount first**:

```bash
sudo umount /mnt/storage
sudo resize2fs /dev/vg_data/lv_storage 50G  # Resize filesystem first
sudo lvreduce -L 50G /dev/vg_data/lv_storage
sudo mount /dev/vg_data/lv_storage /mnt/storage

```

---
