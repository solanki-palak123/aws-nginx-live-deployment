# AWS EC2 Nginx Live Deployment with Custom DNS & SSL ☁️🚀

A hands-on experiment focused on moving beyond local environments (WSL) to deploy a live, secure web server on AWS without spending any money by utilizing cloud Free Tiers.

## 🎯 Project Overview
The goal of this mini-project was to understand the real-world deployment pipeline: launching a cloud server, configuring a web server, mapping a custom domain via DNS records, and securing web traffic with an SSL certificate.

---

## 🛠️ Architecture & Core Components Learned

### 1. Cloud Hosting (AWS EC2)
* Launched a free-tier eligible **Ubuntu Linux EC2 instance** on Amazon Web Services.
* Configured inbound security group rules to open **Port 80 (HTTP)** for web traffic and **Port 22 (SSH)** for remote management.
* Managed private key file permissions using `chmod 400` to satisfy strict Linux security requirements.

### 2. Web Server Configuration (Nginx)
* Installed **Nginx** via the Advanced Package Tool (`apt`).
* Modified the default server blocks (`server_name`) to recognize the inbound custom domain.
* Built and served a custom HTML index page (`index.html`) directly from `/var/www/html/`.

### 3. Domain Name Resolution (DNS)
* Registered a free live second-level domain name using **DuckDNS**.
* Created an **A Record** pointing the custom domain directory straight to the AWS Public IPv4 address (`13.238.217.87`).

### 4. Automated Cyber Security (SSL/HTTPS)
* Installed **Certbot** and its automated Nginx plugin.
* Successfully generated a trusted SSL certificate from **Let's Encrypt**.
* Automatically upgraded all plaintext HTTP requests to encrypted **HTTPS (Port 443)** traffic, achieving a valid "Connection is Secure" status in the browser.

---

## 📋 Commands Handled

```bash
# Secure the private key permissions locally
chmod 400 pree-key.pem

# Securely remote login into the AWS instance
ssh -i "pree-key.pem" ubuntu@YOUR_AWS_PUBLIC_IP

# Update system repositories and install Nginx
sudo apt update && sudo apt install nginx -y

# Configure Nginx server blocks
sudo nano /etc/nginx/sites-available/default
sudo nginx -t
sudo systemctl restart nginx

# Install Certbot and enable automated SSL termination
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d YOUR_DOMAIN.duckdns.org
```

---
