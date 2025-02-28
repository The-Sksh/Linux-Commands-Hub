## **Reset Root Password in Linux**

If you’ve forgotten the **root password**, you can reset it using **single-user mode** or a **live CD**. The steps vary slightly depending on the distribution.

---

## **1️⃣ Method: Using GRUB (For Most Linux Distros)**

### **Step 1: Restart and Enter GRUB Menu**

1. Restart your system.
2. **Press `Esc`**, `Shift`, or `F2` during boot to enter the **GRUB menu**.

---

### **Step 2: Edit GRUB Boot Parameters**

1. Select the default boot entry (`Ubuntu`, `Debian`, `CentOS`, etc.).
2. Press **`e`** to edit the boot command.
3. Find the line starting with **`linux`** or **`linux16`**.
4. Locate `ro quiet splash` or `ro` and replace it with:

Example:
    
    ```
    rw init=/bin/bash
    
    ```
    
    ```
    linux /boot/vmlinuz-xxx root=/dev/sda1 rw init=/bin/bash
    
    ```
    
5. Press `Ctrl + X` or `F10` to boot with the new parameters.

---

### **Step 3: Reset the Root Password**

Now, you’ll have a **root shell** (`#` prompt). Reset the password using:

```bash
passwd root

```

Enter and confirm the new root password.

---

### **Step 4: Reboot**

1. Remount the filesystem:
    
    ```bash
    mount -o remount,rw /
    
    ```
    
2. Reboot the system:

or force reboot:
    
    ```bash
    exec /sbin/init
    
    ```
    
    ```bash
    reboot -f
    
    ```
    

---

## **2️⃣ Method: Using a Live CD (If GRUB is Locked)**

If you **can't access GRUB**, use a **Linux Live CD** or **USB**.

### **Step 1: Boot from a Live CD**

1. Create a bootable USB with **Ubuntu** or any Linux Live ISO.
2. Boot from the USB and open a terminal.

### **Step 2: Mount the Root Partition**

Find your root partition:

```bash
lsblk

```

Mount it:

```bash
sudo mount /dev/sda1 /mnt

```

Change the root environment:

```bash
sudo chroot /mnt

```

### **Step 3: Reset Password**

```bash
passwd root

```

### **Step 4: Reboot**

```bash
exit
sudo reboot

```

---
