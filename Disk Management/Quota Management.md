Quota management in Linux allows administrators to **limit disk usage** for users or groups. This helps prevent a single user from consuming all disk space.

---

## **Step 1: Install Quota Package**

If quota is not installed, install it using:

- **Ubuntu/Debian:**
    
    ```bash
    sudo apt install quota
    
    ```
    
- **RHEL/CentOS:**
    
    ```bash
    sudo yum install quota
    
    ```
    
- **Arch Linux:**
    
    ```bash
    sudo pacman -S quota
    
    ```
    

---

## **Step 2: Enable Quotas on a Filesystem**

### **1. Check the Filesystem**

Use `df -hT` to find the mounted partition:

```bash
df -hT

```

- Example output:
    
    ```
    /dev/sda1   ext4   50G   10G   40G  20%  /
    
    ```
    

### **2. Edit `/etc/fstab`**

Add `usrquota` and `grpquota` to enable quotas:

```bash
sudo nano /etc/fstab

```

Modify the line for `/` or the partition you want to apply quotas to:

```
/dev/sda1  /  ext4  defaults,usrquota,grpquota  0  1

```

Save and exit (`Ctrl + X`, `Y`, `Enter`).

### **3. Remount the Filesystem**

```bash
sudo mount -o remount /

```

---

## **Step 3: Create Quota Database Files**

Run the following commands to create quota files and scan disk usage:

```bash
sudo quotacheck -cum /   # For user quota
sudo quotacheck -cgm /   # For group quota
sudo quotaon -v /        # Enable quotas

```

---

## **Step 4: Set User Quotas**

To set quotas for a user (`john`):

```bash
sudo edquota -u john

```

Example file:

```
Disk quotas for user john (uid 1001):
  Filesystem   blocks   soft   hard   inodes   soft   hard
  /dev/sda1     10000   15000  20000     0       0      0

```

- **soft** = Warning limit
- **hard** = Maximum limit

Save and exit.

To **apply the same quota to multiple users**:

```bash
sudo edquota -p john user2 user3

```

---

## **Step 5: Set Group Quotas**

To set quotas for a group (`developers`):

```bash
sudo edquota -g developers

```

---

## **Step 6: Verify Quotas**

To check a user's quota:

```bash
sudo quota -u john

```

To check a group's quota:

```bash
sudo quota -g developers

```

To check all quotas:

```bash
sudo repquota -a

```

---

## **Step 7: Set Grace Period**

By default, Linux allows a grace period before enforcing limits. Modify it using:

```bash
sudo edquota -t

```

Example:

```
Time limits for file system /dev/sda1:
  Block grace time: 7 days
  Inode grace time: 7 days

```

---
