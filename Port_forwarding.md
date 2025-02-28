### **Port Forwarding in Airtel Router for Linux**

Port forwarding is essential when you want to access services running on a Linux machine from outside your network. Here's a step-by-step guide to configure port forwarding on an **Airtel router**.

---

## **Step 1: Find Your Internal IP Address**

Before configuring the router, you need to know your Linux machine's internal (local) IP.

Run the following command in your terminal:

```bash
ip a | grep inet

```

or

```bash
hostname -I

```

Look for an IP similar to `192.168.1.xxx` (e.g., `192.168.1.100`).

---

## **Step 2: Access Your Airtel Router Settings**

1. Open a web browser and go to:
    
    ```
    http://192.168.1.1
    
    ```
    
2. Log in using your **router’s username and password** (default is usually `admin/admin` or `admin/password`).
    - If you don't know your credentials, check the back of the router or contact Airtel support.

---

## **Step 3: Navigate to Port Forwarding Settings**

1. Go to **Advanced Settings** or **Security**.
2. Look for **NAT (Network Address Translation)** or **Port Forwarding**.
3. Click **Add New Rule** or **Virtual Server**.

---

## **Step 4: Configure the Port Forwarding Rule**

You'll need to enter the following details:

| Field | Value |
| --- | --- |
| **Service Name** | Any name (e.g., SSH, Web, Game Server) |
| **Protocol** | TCP, UDP, or Both (depends on service) |
| **Internal IP** | Your Linux machine's local IP (e.g., `192.168.1.100`) |
| **Internal Port** | The port your service is running on (e.g., `22` for SSH, `80` for Web) |
| **External Port** | The port you want to use from outside (e.g., `2222` for SSH, `8080` for Web) |
| **Enable Rule** | Yes |

**Example: Forward SSH (Port 22)**

- **Internal IP:** `192.168.1.100`
- **Internal Port:** `22`
- **External Port:** `2222`
- **Protocol:** TCP

**Example: Forward Web Server (Port 80)**

- **Internal IP:** `192.168.1.100`
- **Internal Port:** `80`
- **External Port:** `8080`
- **Protocol:** TCP

Click **Save** and **Apply Changes**.

---

## **Step 5: Restart the Router**

After setting up port forwarding, restart your router for changes to take effect.

---

## **Step 6: Allow Ports in Linux Firewall**

Run the following commands on your Linux machine to allow traffic through the forwarded ports.

For SSH (Port 22):

```bash
sudo ufw allow 22/tcp

```

For a Web Server (Port 80):

```bash
sudo ufw allow 80/tcp

```

For a custom external port (e.g., 2222 for SSH):

```bash
sudo ufw allow 2222/tcp

```

Check firewall rules:

```bash
sudo ufw status

```

If using **iptables**, run:

```bash
sudo iptables -A INPUT -p tcp --dport 2222 -j ACCEPT

```

---

## **Step 7: Test Port Forwarding**

From an external network (or using mobile data), try connecting:

For SSH:

```bash
ssh -p 2222 user@your_public_ip

```

For a web server:

```
http://your_public_ip:8080

```

Find your **public IP** using:

```bash
curl ifconfig.me

```

or visit [https://www.whatismyip.com](https://www.whatismyip.com/).

---

## **Troubleshooting**

1. **Check if your Linux service is running**
    
    ```bash
    sudo systemctl status ssh
    sudo systemctl status apache2
    
    ```
    
2. **Verify your public IP is accessible**
    
    ```bash
    nc -zv your_public_ip 2222
    
    ```
    
3. **Check if the router has saved the settings properly.**
4. **Ensure no ISP restrictions (Airtel may block certain ports like 80 or 443).**
Try using non-standard ports like `8080`, `2222`, or `9000`.

---
