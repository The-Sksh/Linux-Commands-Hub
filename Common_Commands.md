Here are **common Linux commands with examples** to help you understand their usage:

---

### **1. File and Directory Management**

| Command | Example | Description |
| --- | --- | --- |
| `ls` | `ls -l /home` | List files in the `/home` directory with details. |
| `cd` | `cd /var/log` | Change directory to `/var/log`. |
| `pwd` | `pwd` | Print the current working directory. |
| `mkdir` | `mkdir new_folder` | Create a directory named `new_folder`. |
| `rmdir` | `rmdir empty_folder` | Remove an empty directory named `empty_folder`. |
| `cp` | `cp file.txt /backup/` | Copy `file.txt` to the `/backup/` directory. |
| `mv` | `mv file.txt /data/` | Move `file.txt` to `/data/`. |
| `rm` | `rm old_file.txt` | Delete `old_file.txt`. |
| `find` | `find / -name file.txt` | Search for `file.txt` starting from `/`. |
| `locate` | `locate config.cfg` | Quickly find the file `config.cfg`. |

---

### **2. File Viewing and Editing**

| Command | Example | Description |
| --- | --- | --- |
| `cat` | `cat file.txt` | Display the contents of `file.txt`. |
| `more` | `more largefile.txt` | View `largefile.txt` one screen at a time. |
| `less` | `less log.txt` | View `log.txt` with navigation options. |
| `head` | `head -n 5 file.txt` | Display the first 5 lines of `file.txt`. |
| `tail` | `tail -n 10 file.txt` | Show the last 10 lines of `file.txt`. |
| `nano` | `nano file.txt` | Edit `file.txt` using Nano. |
| `vim` | `vim file.txt` | Edit `file.txt` using Vim. |

---

### **3. File Permissions**

| Command | Example | Description |
| --- | --- | --- |
| `chmod` | `chmod 755 script.sh` | Set `script.sh` permissions to `755`. |
| `chown` | `chown user:group file.txt` | Change owner and group of `file.txt`. |
| `ls -l` | `ls -l` | List files with permissions. |

---

### **4. Process and System Monitoring**

| Command | Example | Description |
| --- | --- | --- |
| `top` | `top` | View running processes interactively. |
| `htop` | `htop` | Interactive process viewer (if installed). |
| `ps` | `ps aux | grep apache` |
| `kill` | `kill 1234` | Kill the process with PID 1234. |
| `df` | `df -h` | Display disk usage in human-readable format. |
| `du` | `du -sh /var/log` | Show size of `/var/log`. |
| `uptime` | `uptime` | Display system uptime. |
| `free` | `free -h` | Show memory usage in human-readable format. |
| `uname` | `uname -a` | Display system information. |

---

### **5. Networking**

| Command | Example | Description |
| --- | --- | --- |
| `ping` | `ping google.com` | Test connectivity to `google.com`. |
| `ip addr` | `ip addr show` | Show network interfaces and IP addresses. |
| `curl` | `curl https://example.com` | Fetch content from a URL. |
| `wget` | `wget https://example.com/file.zip` | Download `file.zip` from `example.com`. |
| `ssh` | `ssh user@192.168.1.10` | Connect to a remote system via SSH. |
| `scp` | `scp file.txt user@remote:/path/` | Copy `file.txt` to a remote system. |

---

### **6. User Management**

| Command | Example | Description |
| --- | --- | --- |
| `who` | `who` | Display logged-in users. |
| `id` | `id user` | Display user and group IDs for `user`. |
| `adduser` | `sudo adduser newuser` | Add a new user named `newuser`. |
| `passwd` | `passwd newuser` | Set password for `newuser`. |
| `sudo` | `sudo apt update` | Execute `apt update` with root privileges. |

---

### **7. Archiving and Compression**

| Command | Example | Description |
| --- | --- | --- |
| `tar` | `tar -cvf archive.tar /path/to/folder` | Archive `/path/to/folder` into `archive.tar`. |
| `gzip` | `gzip file.txt` | Compress `file.txt` to `file.txt.gz`. |
| `gunzip` | `gunzip file.txt.gz` | Decompress `file.txt.gz`. |
| `zip` | `zip archive.zip file1 file2` | Compress `file1` and `file2` into `archive.zip`. |
| `unzip` | `unzip archive.zip` | Extract `archive.zip`. |

---

### **8. Package Management**

- **Debian-based systems**:
    
    ```bash
    sudo apt update                # Update package lists.
    sudo apt install nginx         # Install Nginx web server.
    sudo apt remove nginx          # Remove Nginx.
    
    ```
    
- **Red Hat-based systems**:
    
    ```bash
    sudo dnf update                # Update packages.
    sudo dnf install httpd         # Install Apache web server.
    sudo dnf remove httpd          # Remove Apache.
    
    ```
    

---

### **9. Disk and Partition Management**

| Command | Example | Description |
| --- | --- | --- |
| `lsblk` | `lsblk` | List block devices. |
| `fdisk` | `sudo fdisk /dev/sda` | Partition the disk `/dev/sda`. |
| `mount` | `sudo mount /dev/sda1 /mnt` | Mount `/dev/sda1` to `/mnt`. |
| `umount` | `sudo umount /mnt` | Unmount the filesystem at `/mnt`. |

---
