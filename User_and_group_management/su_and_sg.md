---

## **1. `su` (Switch User)**

The `su` (substitute user) command allows a user to switch to another user account, including root. By default, it switches to root if no username is provided.

### **Syntax:**

```bash
su [OPTIONS] [USERNAME] [--] [ARGUMENTS]

```

### **Options and Use Cases:**

| Option | Description | Example |
| --- | --- | --- |
| `-` or `-l` | Switches to the user with a full login shell (loads the user's environment and profile). | `su - john` |
| `-c "command"` | Executes a single command as another user. | `su -c "whoami" john` |
| `-s /bin/bash` | Uses a specific shell while switching users. | `su -s /bin/zsh john` |
| `-m` or `-p` | Preserves the current environment variables (does not reset `HOME`, `PATH`, etc.). | `su -m john` |
| `-g GROUP` | Runs the shell with a specified group instead of the default. | `su -g developers - john` |
| `-h` | Displays help information. | `su -h` |
| `-w, --whitelist-environment` | Whitelists specific environment variables. | `su -w PATH,HOME john` |

---

### **`su` Examples:**

### **1. Switch to the root user (default)**

```bash
su

```

🔹 Prompts for the root password and starts a root shell.

### **2. Switch to a specific user (`john`)**

```bash
su john

```

🔹 Prompts for John's password and switches to his shell.

### **3. Switch to `john` but load his full environment**

```bash
su - john

```

🔹 Loads John's full profile, similar to logging in.

### **4. Run a command as `john`**

```bash
su -c "ls -l /home/john" john

```

🔹 Runs the command `ls -l /home/john` as `john`, then returns to the original user.

### **5. Run a command as `john` but keep the current environment**

```bash
su -m -c "echo $HOME" john

```

🔹 Runs `echo $HOME` as `john`, but keeps the original user's home directory.

### **6. Switch to `john` and use a different shell (`zsh`)**

```bash
su -s /bin/zsh john

```

🔹 Switches to `john` and uses `zsh` instead of the default shell.

### **7. Execute multiple commands as another user**

```bash
su -c "whoami; pwd" john

```

🔹 Runs `whoami` and `pwd` as `john`.

### **8. Switch to `john` but use the `developers` group**

```bash
su -g developers - john

```

🔹 Runs `john`'s shell with `developers` as the primary group.

---

## **2. `sg` (Switch Group)**

The `sg` (switch group) command allows users to execute commands under a different group, provided they are a member of that group.

### **Syntax:**

```bash
sg [OPTIONS] GROUPNAME [--] COMMAND

```

### **Options and Use Cases:**

| Option | Description | Example |
| --- | --- | --- |
| `-c "command"` | Executes a command under the specified group. | `sg developers -c "touch /tmp/devfile.txt"` |
| `-` | Starts a new shell under the specified group. | `sg admin` |

---

### **`sg` Examples:**

### **1. Run a command as the `developers` group**

```bash
sg developers -c "mkdir /home/devs/shared"

```

🔹 Runs `mkdir /home/devs/shared` as a member of `developers`.

### **2. Create a file as the `admin` group**

```bash
sg admin -c "touch /var/log/adminlog.txt"

```

🔹 Runs `touch` as a member of `admin`.

### **3. Start a new shell as `finance` group**

```bash
sg finance

```

🔹 Opens a new shell where `finance` is the primary group.

### **4. Run multiple commands as `developers`**

```bash
sg developers -c "cd /home/devs && ls -l"

```

🔹 Changes to `/home/devs` and lists files as `developers`.

---

## **Key Differences: `su` vs `sg`**

| Feature | `su` (Switch User) | `sg` (Switch Group) |
| --- | --- | --- |
| Purpose | Switches to another user | Runs commands under a specific group |
| Authentication | Requires user password | No password needed if already a group member |
| Shell Access | Can start a new shell | Only executes a command (does not start a new shell) |
| Common Use | Switching users or running commands as another user | Running commands under a different group |

---

## **When to Use `su` vs `sg`?**

- **Use `su` when** you need to switch to another user account or run commands as another user.
- **Use `sg` when** you need to execute commands as a specific group but stay as the same user.
