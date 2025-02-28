# **Disk Operations in Linux**

Disk management in Linux involves tasks like **listing disks, partitioning, formatting, mounting, and monitoring disk usage**. Below are the essential commands and tools for managing disks in Linux.

---

## **1️⃣ List Disks and Partitions**

To view available disks and their partitions, use:

### **Check All Disks and Partitions**

```bash
lsblk

```

- Shows all disk drives (`sda`, `sdb`, etc.) and partitions (`sda1`, `sda2`, etc.).
- Example output:
    
    ```
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda      8:0    0  500G  0 disk
    ├─sda1   8:1    0  250G  0 part /
    ├─sda2   8:2    0  249G  0 part /home
    ├─sda3   8:3    0    1G  0 part [SWAP]
    
    ```
    

### **Check Disk Space Usage**

```bash
df -h

```

- Shows disk space usage in a human-readable format.

### **Check Disk Information**

```bash
fdisk -l

```

- Lists disk partitions, sizes, and types.

### **Check Filesystem Types**

```bash
lsblk -f

```

- Displays mounted filesystems and labels.

---

## **2️⃣ Partitioning Disks**

You can use **fdisk**, **parted**, or **cfdisk** to create and manage partitions.

### **Using `fdisk`**

1. Open `fdisk` for a specific disk (e.g., `/dev/sdb`):
    
    ```bash
    sudo fdisk /dev/sdb
    
    ```
    
2. Press:
    - `n` → Create a new partition.
    - `d` → Delete a partition.
    - `p` → Print the partition table.
    - `w` → Write changes and exit.

### **Using `parted` (for GPT Disks)**

1. Start `parted`:
    
    ```bash
    sudo parted /dev/sdb
    
    ```
    
2. Create a **GPT partition table**:
    
    ```bash
    mklabel gpt
    
    ```
    
3. Create a **new partition**:
    
    ```bash
    mkpart primary ext4 0% 100%
    
    ```
    
4. Exit:
    
    ```bash
    quit
    
    ```
    

---

## **3️⃣ Formatting Partitions**

After partitioning, format the new partition with a filesystem.

### **Format as ext4**

```bash
sudo mkfs.ext4 /dev/sdb1

```

### **Format as xfs**

```bash
sudo mkfs.xfs /dev/sdb1

```

### **Format as FAT32 (for USB drives)**

```bash
sudo mkfs.vfat -F32 /dev/sdb1

```

---

## **4️⃣ Mounting and Unmounting Disks**

To access a partition, mount it to a directory.

### **Mount a Partition**

```bash
sudo mount /dev/sdb1 /mnt

```

### **Unmount a Partition**

```bash
sudo umount /mnt

```

### **Make the Mount Permanent**

Edit **`/etc/fstab`** to automatically mount the partition at boot:

```bash
sudo nano /etc/fstab

```

Add a line:

```
/dev/sdb1  /mnt  ext4  defaults  0  2

```

Save and exit (`Ctrl + X`, `Y`, `Enter`).

---

## **5️⃣ Swap Partition Management**

### **Create a Swap Partition**

```bash
sudo mkswap /dev/sdb3

```

### **Enable Swap**

```bash
sudo swapon /dev/sdb3

```

### **Disable Swap**

```bash
sudo swapoff /dev/sdb3

```

### **Make Swap Permanent**

Add this to `/etc/fstab`:

```
/dev/sdb3 none swap sw 0 0

```

---

## **6️⃣ Monitoring Disk Usage**

### **Check Disk Usage of Directories**

```bash
du -sh /var/log

```

### **Check Free Space on Filesystem**

```bash
df -h

```

### **Monitor Disk I/O Performance**

```bash
iostat -x 1

```

*(Requires `sysstat` package: `sudo apt install sysstat`)*

---

## **7️⃣ Check and Repair Filesystems**

If a filesystem gets corrupted, check and repair it.

### **Check Filesystem Health**

```bash
sudo fsck /dev/sdb1

```

### **Repair Errors Automatically**

```bash
sudo fsck -y /dev/sdb1

```

---
