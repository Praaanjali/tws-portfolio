# demo-actions-project
## 🧩 Prerequisites

- AWS Account
- Registered domain (GoDaddy, Namecheap, or Route53)
- Static site files (`index.html`, `style.css`, etc.)
- GitHub account (`praaanjali`)
- Security group allowing ports: **22 (SSH)**, **80 (HTTP)**, **443 (HTTPS)**

---

## 🚀 Step 1: Launch EC2 Instance

1. Go to **AWS Console → EC2 → Launch Instance**
2. Choose **Ubuntu 22.04 LTS**
3. Instance type: `t2.micro`
4. Configure inbound rules for SSH, HTTP, and HTTPS
5. Connect to instance:
   ```bash
   ssh -i your-key.pem ubuntu@<EC2-PUBLIC-IP>
   
   ```

---

## ⚙️ Step 2: Install Nginx

```bash
sudo apt update && sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```

---

## 📁 Step 3: Deploy Your Static Website

### Option 1: Copy files manually
```bash
sudo rm -rf /var/www/html/*
sudo cp -r ~/your-static-site/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html
```

### Option 2: Clone from GitHub
```bash
cd /home/ubuntu
git clone https://github.com/Praaanjali/tws-portfolio.git
sudo cp -r * /var/www/html/

```

---


## 🌍 Step 4 : Configure DNS Records

| Type | Name | Value |
|------|------|--------|
| A | @ | <EC2-PUBLIC-IP> |
| A | www | <EC2-PUBLIC-IP> |

➡️ Wait 5–10 minutes for DNS propagation.

---

## 🔒 Step 5:Install SSL Certificate (Let's Encrypt)

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d example.com -d www.example.com
```

- Select **redirect option** for automatic HTTP → HTTPS redirection.

---

## ✅ Step 6: Verify HTTPS

Visit:
```
https://example.com
```
You should see your static site with a **padlock icon** in the browser.

---


## 🧑‍💻 Step 7: Push Code to GitHub

```bash
git init
git add .
git commit -m "Static website deployment with Nginx and SSL"
git branch -M main
git remote add origin https://github.com/praaanjali/static-website-nginx.git
git push -u origin main
```
