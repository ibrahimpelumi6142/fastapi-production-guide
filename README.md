# 🚀 FastAPI Production Deployment Guide (Linux VPS)

![FastAPI Deployment Banner](BANNER_IMAGE_URL)

A complete, production-ready guide explaining how to deploy **FastAPI** to a **VPS** using:

* **Nginx** (reverse proxy + HTTPS)
* **Gunicorn** (process manager)
* **Uvicorn workers**
* **Systemd** (auto-restart services)
* **Environment variables**
* **Secure folder structure**

This is the exact setup used in many real SaaS and automation backends.

---

## 📦 Project Structure

```
fastapi-production-guide/
├── app/
│   └── main.py
├── nginx/
│   └── fastapi.conf
├── systemd/
│   └── fastapi.service
├── .env.example
├── requirements.txt
└── README.md
```

---

## 1️⃣ Install Dependencies

```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip nginx git
```

---

## 2️⃣ Clone & Setup Project

```bash
git clone https://github.com/ibrahimpelumi6142/fastapi-production-guide
cd fastapi-production-guide

python3 -m venv venv
source venv/bin/activate

pip install -r requirements.txt
```

---

## 3️⃣ Start FastAPI With Gunicorn

```bash
gunicorn -k uvicorn.workers.UvicornWorker app.main:app --bind 0.0.0.0:8000 --workers 3
```

---

## 4️⃣ Create Systemd Service (Auto-restart + start on boot)

```bash
sudo cp systemd/fastapi.service /etc/systemd/system/fastapi.service
sudo systemctl daemon-reload
sudo systemctl start fastapi
sudo systemctl enable fastapi
```

Check logs:

```bash
journalctl -u fastapi -f
```

---

## 5️⃣ Configure Nginx Reverse Proxy

```bash
sudo cp nginx/fastapi.conf /etc/nginx/sites-available/
sudo ln -s /etc/nginx/sites-available/fastapi.conf /etc/nginx/sites-enabled/

sudo nginx -t
sudo systemctl restart nginx
```

---

## 6️⃣ Add HTTPS (Free SSL)

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d YOUR_DOMAIN
```

---

## 7️⃣ Environment Variables

`.env.example` included.

---

## 8️⃣ Deploy Updates

```bash
git pull
source venv/bin/activate
pip install -r requirements.txt
sudo systemctl restart fastapi
```

---

# ✨ Author

**Lasisi Ibrahim Pelumi**
- Full-stack engineer & automation developer
- Creator of **WorqNow – WhatsApp AI Job Assistant**

---

# ⭐ If this repo helped you, please give it a star!
