# **Permanent Mounting of a Partition in Linux**

To permanently mount a partition in Linux, you need to update the `/etc/fstab` file so that the partition is automatically mounted at boot.

---

## **Step 1: Identify the Partition**

First, check the partition details:

```bash
lsblk -f

```

or

```bash
sudo blkid

```

- Example output:
    
    ```
    /dev/sdb1: UUID="a1b2c3d4-5678" TYPE="ext4"
    
    ```
    

🔹 **Take note of the UUID** (e.g., `a1b2c3d4-5678`).

---

## **Step 2: Create a Mount Point**

Choose where to mount the partition (e.g., `/mnt/data` or `/home/user/disk`).

```bash
sudo mkdir -p /mnt/data

```

---

## **Step 3: Edit `/etc/fstab`**

1. Open `/etc/fstab` with a text editor:
    
    ```bash
    sudo nano /etc/fstab
    
    ```
    
2. Add a new line at the bottom:
    
    ```
    UUID=a1b2c3d4-5678  /mnt/data  ext4  defaults  0  2
    
    ```
    
    - Replace `a1b2c3d4-5678` with your actual **UUID**.
    - Replace `ext4` with the **filesystem type** (`xfs`, `vfat`, etc.).
    - **Options** (`defaults` means read/write, async, auto-mount).

---

## **Step 4: Apply Changes**

1. **Remount all partitions** (to test `fstab`):
    
    ```bash
    sudo mount -a
    
    ```
    
2. **Verify the mount**:
    
    ```bash
    df -h
    
    ```
    

---

## **Step 5: Test Reboot**

Reboot your system to confirm the partition mounts automatically:

```bash
sudo reboot

```

After reboot, check if it’s still mounted:

```bash
df -h

```

✅ **Done!** Your partition will now be mounted permanently at boot. 🚀
