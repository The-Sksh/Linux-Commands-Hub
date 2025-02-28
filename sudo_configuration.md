## **Sudo Configuration in Linux**

`sudo` (Superuser Do) allows permitted users to execute commands as root or another user. The `sudo` command is configured using the **sudoers** file.

---

### **1️⃣ Checking Sudo Access**

To check if you have `sudo` privileges, run:

```bash
sudo -v

```

If you don’t have sudo access, you'll see a **Permission denied** error.

---

### **2️⃣ Adding a User to the Sudo Group**

To grant a user sudo privileges, run:

```bash
sudo usermod -aG sudo username

```

For **CentOS/RHEL**, use:

```bash
sudo usermod -aG wheel username

```

Then, verify:

```bash
groups username

```

---

### **3️⃣ Editing the Sudoers File (Safely)**

To modify sudo permissions, always use:

```bash
sudo visudo

```

This ensures syntax checking before saving.

---

### **4️⃣ Granting Full Sudo Access**

Add the following line at the end:

```bash
username ALL=(ALL:ALL) ALL

```

This allows `username` to run **any command** as root.

For password-less sudo:

```bash
username ALL=(ALL) NOPASSWD: ALL

```

---

### **5️⃣ Restricting Sudo Access to Specific Commands**

Example: Allow `username` to run only `apt update` and `systemctl restart apache2`:

```bash
username ALL=(ALL) NOPASSWD: /usr/bin/apt update, /bin/systemctl restart apache2

```

---

### **6️⃣ Creating a Custom Sudoers File**

Instead of modifying `/etc/sudoers`, create a file in `/etc/sudoers.d/`:

```bash
sudo visudo -f /etc/sudoers.d/custom_user

```

Add:

```bash
username ALL=(ALL) NOPASSWD: /sbin/reboot

```

This grants permission **only** for rebooting.

---

### **7️⃣ Testing Sudo Configuration**

After making changes, test them:

```bash
sudo -l -U username

```

This lists allowed sudo commands.

---

### **8️⃣ Removing Sudo Access**

To remove a user from sudo access:

```bash
sudo deluser username sudo  # Debian/Ubuntu
sudo gpasswd -d username wheel  # RHEL/CentOS

```

---
