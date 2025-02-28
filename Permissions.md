---

### 1. **Linux Permissions**

- Each file and directory in Linux has three types of permissions:
    - **Read (`r`)** → View file contents (`4`)
    - **Write (`w`)** → Modify file contents (`2`)
    - **Execute (`x`)** → Run file as a program (`1`)
- These permissions are assigned to three categories:
    - **Owner (`u`)** → The file's creator
    - **Group (`g`)** → Users in the same group
    - **Others (`o`)** → All other users

**Syntax:**

```bash
ls -l filename

```

**Example Output:**

```bash
-rwxr-xr--  1 user group 1234 Jul 9 10:00 script.sh

```

- `rwx` → Owner has read, write, and execute permissions.
- `r-x` → Group has read and execute permissions.
- `r--` → Others have only read permission.

---

### 2. **chown and chmod Command in Linux**

### **chown (Change Ownership)**

- Used to change the owner and/or group of a file.

**Syntax:**

```bash
chown new_owner:new_group filename

```

**Example:**

```bash
chown bob:developers file.txt  # Changes owner to "bob" and group to "developers"

```

### **chmod (Change Permissions)**

- Used to modify read, write, and execute permissions.
- Can be used in **symbolic mode** (`u`, `g`, `o`, `+`, ``, `=`) or **numeric mode** (`777`, `644`, etc.).

**Syntax:**

```bash
chmod [mode] filename

```

**Example:**

```bash
chmod 755 script.sh   # Owner has full permissions, others have read and execute
chmod u+w file.txt    # Adds write permission for the owner
chmod g-x script.sh   # Removes execute permission for the group
chmod o=r file.txt    # Sets read-only permission for others

```

---

### 3. **chmod Command in Linux**

**Common Permission Numbers:**

- `777` → Everyone can read, write, and execute.
- `755` → Owner can read, write, execute; others can only read and execute.
- `644` → Owner can read and write; others can only read.
- `600` → Owner can read and write; no permissions for others.
- `400` → Read-only for the owner, no access for others.

**Examples:**

```bash
chmod 700 private.sh   # Only owner has all permissions
chmod 600 secret.txt   # Only owner can read/write
chmod 444 report.log   # Read-only for everyone

```

---

### 4. **Special Permissions in Linux**

### **Setuid (SUID)**

- If set on an executable file, the process runs as the file’s owner, not the executing user.
- Commonly used for system binaries like `passwd`.

**Syntax:**

```bash
chmod u+s filename

```

**Example:**

```bash
chmod 4755 /bin/su  # Allows the file to execute as the owner (usually root)

```

**Check SUID files:**

```bash
find / -perm -4000 -type f 2>/dev/null

```

### **Setgid (SGID)**

- If set on a directory, new files inherit the group of the directory instead of the creator’s group.

**Syntax:**

```bash
chmod g+s directory

```

**Example:**

```bash
chmod 2755 /shared   # Ensures all files in "shared" inherit the group

```

**Check SGID files:**

```bash
find / -perm -2000 -type f 2>/dev/null

```

### **Sticky Bit**

- Prevents users from deleting files they don’t own in a shared directory (e.g., `/tmp`).

**Syntax:**

```bash
chmod +t directory

```

**Example:**

```bash
chmod 1777 /tmp  # Ensures only file owners can delete their files

```

**Check Sticky Bit directories:**

```bash
find / -type d -perm -1000

```

---

### 5. **Setgid and Sticky Bit**

**Example 1: Setting SGID on a Shared Directory**

```bash
mkdir /project
chmod 2775 /project
chown :developers /project

```

- Any new file created inside `/project` will have the `developers` group.

**Example 2: Secure Temporary Directory with Sticky Bit**

```bash
chmod 1777 /var/tmp

```

- All users can create files in `/var/tmp`, but only the owner can delete them.

---
