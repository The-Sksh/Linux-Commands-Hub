### **Access Control Lists (ACL) in Linux**

**ACL (Access Control List)** provides **fine-grained file permissions** beyond the standard **rwx** model, allowing **specific users or groups** to have custom access.

---

## **1. Checking ACL Support**

Before using ACL, ensure your filesystem supports it.

Check with:

```bash
mount | grep acl

```

If ACL is not enabled, remount with:

```bash
mount -o remount,acl /mountpoint

```

---

## **2. Viewing ACL of a File**

To check ACL permissions on a file or directory:

```bash
getfacl filename

```

**Example:**

```bash
getfacl myfile.txt

```

**Output:**

```
# file: myfile.txt
# owner: user1
# group: users
user::rw-
user:john:r--
group::r--
mask::rw-
other::r--

```

---

## **3. Setting ACL Permissions**

### **a) Granting Permissions to a User**

```bash
setfacl -m u:username:permissions filename

```

**Example:**

```bash
setfacl -m u:john:rw myfile.txt

```

This gives **read (`r`) and write (`w`)** permissions to `john`.

### **b) Granting Permissions to a Group**

```bash
setfacl -m g:groupname:permissions filename

```

**Example:**

```bash
setfacl -m g:developers:rwx project_dir

```

Now, all users in the `developers` group have **full (`rwx`)** access to `project_dir`.

### **c) Assigning Default ACL (Inherited Permissions)**

```bash
setfacl -d -m u:john:rw directory/

```

This ensures all **new files** created inside `directory/` inherit `john`’s **read-write** access.

---

## **4. Removing ACL Permissions**

### **a) Remove a Specific User's ACL**

```bash
setfacl -x u:username filename

```

**Example:**

```bash
setfacl -x u:john myfile.txt

```

Removes `john`'s special permissions on `myfile.txt`.

### **b) Remove All ACL Entries**

```bash
setfacl -b filename

```

**Example:**

```bash
setfacl -b myfile.txt

```

Removes **all ACL entries**, keeping only standard file permissions.

---

## **5. Recursive ACL Operations**

To apply ACL changes **recursively** to all files in a directory:

```bash
setfacl -R -m u:john:rwx /shared_folder

```

---

## **6. Checking Files with ACL**

To find all files with ACL enabled:

```bash
find / -exec getfacl {} + 2>/dev/null | grep "user:"

```

---

### **Use Case Examples**

🔹 **Allow "alex" to edit a file without changing group ownership:**

```bash
setfacl -m u:alex:rw confidential.txt

```

🔹 **Give "developers" group full control over a directory:**

```bash
setfacl -m g:developers:rwx /projects

```

🔹 **Ensure all new files in `/team_docs` inherit ACL settings:**

```bash
setfacl -d -m g:team:rwx /team_docs

```

---

### #Note :

ACLs provide **more flexible permissions** than standard Linux file permissions. They are useful for managing multi-user access without modifying file ownership or primary groups.
