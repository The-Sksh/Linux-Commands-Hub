# **Linux Shell**

---

In Linux, a shell is a command-line interface that allows users to interact with the operating system. It serves as an intermediary between the user and the kernel, enabling command execution, scripting, and automation. Linux offers various shells, each with unique features and capabilities.

---

## **Common Shells in Linux**

### **sh (Bourne Shell)**

- Focused on executing commands and writing basic scripts.
- Minimal interactive features compared to modern shells.
- Supports variables, loops, conditionals, and redirection.

### **Bash (Bourne Again Shell)**

- Default shell in most Linux distributions.
- Combines features of the Bourne shell (`sh`) with additional improvements.
- Supports scripting, command history, tab completion, and more.

### **Ksh (Korn Shell)**

- Combines features of `sh` and `csh` (C Shell).
- Known for scripting capabilities and performance in programming environments.

### **Tcsh (TENEX C Shell)**

- An enhanced version of the C shell (`csh`).
- Provides features like command-line editing and spelling correction.

### **Fish (Friendly Interactive Shell)**

- Focuses on user-friendliness and interactive use.
- Offers syntax highlighting, autosuggestions, and a rich set of built-in commands.

### **Zsh (Z Shell)**

- Powerful and customizable shell.
- Includes advanced features like shared history, spell-checking, and themes.
- Compatible with Bash scripts and offers additional capabilities.

### **Dash (Debian Almquist Shell)**

- Lightweight and fast.
- Often used as the default `/bin/sh` in some systems for scripting due to its efficiency.

---

### **Useful Shell Commands**

- **`cat /etc/shells`**: Displays a list of valid shells installed on the system.
- **`echo $SHELL`**: Displays the path of your current default login shell.

---

## **Working with YUM**

### **Installing Bash**

```bash
yum install Bash*

```

- Installs all packages starting with "Bash" from the configured repositories.

### **Searching for Bash Packages**

```bash
yum search Bash

```

- Searches the repositories for packages with "Bash" in their name or description.

### **Troubleshooting Missing Packages**

If `yum search Bash` doesn't list certain packages:

1. **Enable Additional Repositories:**
    
    ```bash
    yum install epel-release
    
    ```
    
2. **Update Repository Cache:**
    
    ```bash
    yum makecache
    
    ```
    
3. **Search with Broader Keywords:**
    
    ```bash
    yum search color prompt
    
    ```
    

---

## **Using grc (Generic Colourizer)**

**grc** adds color to command-line outputs for easier readability.

### **Steps to Install grc**

1. **Download grc from GitHub**:
    
    ```bash
    wget https://github.com/garabik/grc/archive/refs/tags/v1.13.tar.gz
    
    ```
    
2. **Extract the File**:
    
    ```bash
    tar -xvf v1.13.tar.gz
    
    ```
    
3. **Move the Folder to `/opt/`**:
    
    ```bash
    mv grc-1.13 /opt/
    
    ```
    
4. **Run the Installation Script**:
    
    ```bash
    cd /opt/grc-1.13
    ./install.sh
    
    ```
    

### **Enable Persistent Colorized Output**

1. **Copy the Script**:
    
    ```bash
    cp -v /opt/grc-1.13/grc.sh /etc
    
    ```
    
2. **Edit `.bashrc`**:

Add:
    
    ```bash
    vim ~/.bashrc
    
    ```
    
    ```bash
    GRC_ALIASES=true
    [[ -s "/etc/profile.d/grc.sh" ]] && source /etc/grc.sh
    
    ```
    
3. **Apply Changes**:
    
    ```bash
    source ~/.bashrc
    
    ```
    

---

## **Installing and Configuring Zsh**

### **Install Zsh**

```bash
yum install zsh*

```

### **Verify Installation**

```bash
cat /etc/shells

```

### **Configure Zsh**

1. **Edit `.zshrc`**:

Add:
    
    ```bash
    vim ~/.zshrc
    
    ```
    
    ```bash
    export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
    export GOROOT=/usr/local/go
    [[ -s "/etc/grc.zsh" ]] && source /etc/grc.zsh
    
    ```
    
2. **Change Default Shell to Zsh**:
    
    ```bash
    chsh -s $(which zsh)
    
    ```
    
3. **Reload Configuration**:
    
    ```bash
    source ~/.zshrc
    
    ```
    

---

### **Conclusion**

The steps provided cover installing and customizing Linux shells, using `grc` for colorized output, and configuring `Zsh` for an enhanced command-line experience.
