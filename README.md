# Save the complete README content to a file for download
readme_content = """# 🌐 Lab Guide: Deploying Web Applications with LEMP and LAMP Stack

---

## 📚 A. Pre-Lab Knowledge

### 1. Reverse Proxy

![Reverse Proxy Flow](reverse-proxy-flow.png)

A **Reverse Proxy** is a server that receives requests from clients and forwards them to the appropriate web server. Benefits include:

- Hiding real web server IP to prevent direct DDoS attacks
- Load balancing to optimize server resource usage

### 2. LAMP vs LEMP Stack

#### 🔹 LAMP Stack
- **L**inux
- **A**pache
- **M**ySQL
- **P**HP

Apache is used as the web server, PHP for backend logic, and MySQL for the database.

#### 🔹 LEMP Stack
- **L**inux
- **E**ngine-X (Nginx)
- **M**ySQL
- **P**HP

Nginx replaces Apache. It's faster and better for serving static content, while Apache is more feature-rich for dynamic sites.

---

## 🧪 B. Lab Instructions

### OS Template: `Ubuntu-Server-22.04-x64`

---

## 🧱 I. Deploying LEMP Stack for WordPress

### 1. Installation Steps

#### 📥 1.1 Install Nginx
```bash
sudo apt update
sudo apt install nginx
sudo systemctl enable nginx
sudo systemctl start nginx
