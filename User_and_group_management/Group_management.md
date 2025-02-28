In Linux, you can create a new group using the `groupadd` command. Here’s how:

### 1. **Create a New Group**

```bash
sudo groupadd groupname

```

This creates a new group named `groupname`.

### 2. **Verify Group Creation**

```bash
cat /etc/group | grep groupname

```

### 3. **Add a User to a Group**

```bash
sudo usermod -aG groupname username

```

- `aG`: Appends the user to the group without removing them from other groups.

### 4. **List Groups a User Belongs To**

```bash
groups username

```

or

```bash
id username

```

### 5. **Delete a Group**
