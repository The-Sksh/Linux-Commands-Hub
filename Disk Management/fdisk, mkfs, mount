In Linux, you use `fdisk` to **partition** a disk, `mkfs` to **format** a partition, and `mount` to **attach** the partition to a directory. Below is a **step-by-step guide** to creating, formatting, and mounting a new disk in Linux.

---

## **Step 1: Identify Available Disks**

Before modifying disk partitions, check the available disks using:

```bash
lsblk

```

or

```bash
sudo fdisk -l

```

- Example output:
    
    ```
    Disk /dev/sdb: 50 GB, 50000000000 bytes
    Disk model: Virtual Disk
    
    ```
    

🔹 In this case, `/dev/sdb` is the new disk.

---

## **Step 2: Partition the Disk using `fdisk`**

1. Run `fdisk` on the disk:
    
    ```bash
    sudo fdisk /dev/sdb
    
    ```
    
2. Inside `fdisk`, enter the following commands:
    - `n` → Create a new partition.
    - `p` → Select primary partition (default).
    - Press **Enter** to accept the default partition number.
    - Press **Enter** to accept the default first sector.
    - Press **Enter** to accept the default last sector (uses the whole disk).
    - `w` → Write changes and exit.

🔹 Now the partition `/dev/sdb1` is created.

---

## **Step 3: Format the Partition using `mkfs`**

After partitioning, format it with a filesystem.

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

## **Step 4: Mount the Partition using `mount`**

Create a mount point and mount the partition.

1. **Create a directory to mount the disk**:
    
    ```bash
    sudo mkdir /mnt/mydisk
    
    ```
    
2. **Mount the partition**:
    
    ```bash
    sudo mount /dev/sdb1 /mnt/mydisk
    
    ```
    
3. **Verify the mount**:
    
    ```bash
    df -h
    
    ```
    
    - The new disk should be listed under `/mnt/mydisk`.

---

## **Step 5: Make the Mount Permanent (`/etc/fstab`)**

To automatically mount the disk at boot, add an entry to `/etc/fstab`:

1. **Get the UUID of the partition**:
    
    ```bash
    sudo blkid /dev/sdb1
    
    ```
    
    - Example output:
        
        ```
        /dev/sdb1: UUID="a1b2c3d4-5678" TYPE="ext4"
        
        ```
        
2. **Edit `/etc/fstab`**:
    
    ```bash
    sudo nano /etc/fstab
    
    ```
    
3. **Add this line** (replace UUID with actual value):
    
    ```
    UUID=a1b2c3d4-5678  /mnt/mydisk  ext4  defaults  0  2
    
    ```
    
4. **Save and exit (`Ctrl + X`, `Y`, `Enter`)**.
5. **Test the configuration**:
    
    ```bash
    sudo mount -a
    
    ```
    

---

## **Step 6: Unmount the Partition**

To unmount the partition, use:

```bash
sudo umount /mnt/mydisk

```

---

##
