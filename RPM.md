**RPM (Red Hat Package Manager)** is the default package management system for **RHEL, CentOS, Fedora**, and other Red Hat-based distributions. It is used to install, update, remove, and verify software packages.

---

## **1. Checking RPM Version**

```bash
rpm --version

```

---

## **2. Installing an RPM Package**

If you have an `.rpm` package file, install it using:

```bash
sudo rpm -ivh package-name.rpm

```

- `i` → Install
- `v` → Verbose output
- `h` → Show progress

Example:

```bash
sudo rpm -ivh httpd-2.4.6-97.el7.centos.x86_64.rpm

```

---

## **3. Upgrading an RPM Package**

To upgrade an already installed package:

```bash
sudo rpm -Uvh package-name.rpm

```

- This installs the package if not already installed.

---

## **4. Removing an RPM Package**

To remove a package:

```bash
sudo rpm -e package-name

```

Example:

```bash
sudo rpm -e httpd

```

---

## **5. Querying Installed Packages**

### **Check if a Package is Installed**

```bash
rpm -q package-name

```

Example:

```bash
rpm -q httpd

```

### **List All Installed Packages**

```bash
rpm -qa

```

### **Get Package Information**

```bash
rpm -qi package-name

```

Example:

```bash
rpm -qi httpd

```

### **List Files in an Installed Package**

```bash
rpm -ql package-name

```

Example:

```bash
rpm -ql httpd

```

---

## **6. Verifying and Checking Dependencies**

### **Verify an Installed Package**

```bash
rpm -V package-name

```

### **Check Package Dependencies**

```bash
rpm -qR package-name

```

Example:

```bash
rpm -qR httpd

```

---

## **7. Extract Files from an RPM Package**

```bash
rpm2cpio package-name.rpm | cpio -idmv

```

---

## **8. Using `yum` or `dnf` for Dependency Resolution**

RPM does **not** resolve dependencies automatically. Instead, use:

For **CentOS 7/RHEL 7** and older:

```bash
sudo yum install package-name

```

For **CentOS 8/RHEL 8** and newer:

```bash
sudo dnf install package-name

```

---
