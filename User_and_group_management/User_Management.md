In Linux, you can create a new user using the `useradd` or `adduser` command. Here’s how:

### 1. **Using `useradd` (Basic Command)**

```bash
sudo useradd -m newusername
sudo passwd newusername

```

- `m`: Creates a home directory for the user.
- `passwd newusername`: Sets the password for the new user.

### 2. **Using `adduser` (More Interactive)**

```bash
sudo adduser newusername

```

This will prompt you to enter a password and some additional user details.

### 3. **Adding User to Sudo Group (Optional)**

If you want the user to have admin privileges:

```bash
sudo usermod -aG sudo newusername  # For Debian/Ubuntu
sudo usermod -aG wheel newusername # For RHEL/CentOS

```

### 4. **Verify User Creation**

Check the `/etc/passwd` file:

```bash
cat /etc/passwd | grep newusername

```

## User modification

The `usermod` command in Linux is used to modify user accounts. Below are some common usages:

### 1. **Change Username**

```bash
sudo usermod -l newusername oldusername

```

This renames `oldusername` to `newusername`.

### 2. **Change User Home Directory**

```bash
sudo usermod -d /new/home/directory -m username

```

- `d /new/home/directory`: Sets the new home directory.
- `m`: Moves existing files to the new directory.

### 3. **Add User to a Group**

```bash
sudo usermod -aG groupname username

```

- `aG`: Adds the user to the specified group without removing them from other groups.

### 4. **Change User's Primary Group**

```bash
sudo usermod -g newgroup username

```

- Changes the user's primary group.

### 5. **Lock a User Account**

```bash
sudo usermod -L username

```

- Locks the user account (prevents login).

### 6. **Unlock a User Account**

```bash
sudo usermod -U username

```

- Unlocks the user account.

### 7. **Change User's Shell**

```bash
sudo usermod -s /bin/bash username

```

- Changes the user's default shell.

### 8. **Expire User Account**

```bash
sudo usermod -e YYYY-MM-DD username

```

- Sets an expiration date for the user account.
