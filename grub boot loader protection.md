## **Protect GRUB Boot Loader with a Password**

To **secure the GRUB boot loader**, you can set a **GRUB password** to prevent unauthorized users from modifying boot parameters or accessing **single-user mode**.

---

## **1️⃣ Set a Password for GRUB**

### **Step 1: Generate a GRUB Password Hash**

Run the following command to generate a hashed password:

```bash
grub-mkpasswd-pbkdf2

```

- Enter a strong password when prompted.
- The output will be:
*(Copy this hash, as you'll need it in the next step.)*
    
    ```
    PBKDF2 hash of your password is grub.pbkdf2.sha512.10000.ABCD...XYZ
    
    ```
    

---

### **Step 2: Edit GRUB Configuration**

Open the GRUB custom configuration file:

```bash
sudo nano /etc/grub.d/40_custom

```

Add these lines at the beginning:

```bash
set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.ABCD...XYZ

```

*(Replace `ABCD...XYZ` with your actual hash.)*

This sets `"admin"` as the superuser and requires a password for modifying boot settings.

---

### **Step 3: Protect Boot Entries**

To **restrict normal users** from booting specific entries, modify the `/etc/grub.d/10_linux` file:

```bash
sudo nano /etc/grub.d/10_linux

```

Find the line:

```bash
echo "menuentry ..."

```

Modify it to include `--unrestricted` or `--users`:

```bash
echo "menuentry 'Ubuntu' --users admin {"

```

- `-unrestricted` → Allows all users to boot but prevents modifications.
- `-users admin` → Requires authentication to boot.

---

### **Step 4: Update GRUB Configuration**

Save the file (`Ctrl + X`, then `Y` and `Enter`), then update GRUB:

```bash
sudo update-grub   # Ubuntu/Debian
sudo grub2-mkconfig -o /boot/grub2/grub.cfg   # CentOS/RHEL

```

---

## **2️⃣ Restrict Access to GRUB Configuration**

Change permissions on the GRUB configuration file to prevent unauthorized modifications:

```bash
sudo chmod 600 /boot/grub/grub.cfg

```

---

## **3️⃣ Verify GRUB Protection**

1. Reboot the system:
    
    ```bash
    sudo reboot
    
    ```
    
2. When the **GRUB menu** appears, press `e` to edit a boot entry.
3. GRUB will now prompt for the **admin password** before allowing modifications.

---

## Note :

Now, **only authorized users** can modify GRUB settings, preventing unauthorized access to system boot options.
