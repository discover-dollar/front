# 🚀 Full Stack Docker Setup (Angular + Node + Mongo + Nginx)

This document explains the complete setup for running:

- Angular Frontend (Development mode using `ng serve`)
- Node.js + Express Backend
- MongoDB
- Nginx (running on host machine)
- Separate repositories for frontend and backend
- Separate Docker Compose files
- Shared Docker network
- No mixing of repositories

---

# 🏗 Architecture Overview

Browser
   ↓
Nginx (Port 80 - Host Machine)
   ↓
---------------------------------
| Frontend Container (8081)     |
| Angular - ng serve            |
---------------------------------
| Backend Container (8082)      |
| Node + Express API            |
---------------------------------
| Mongo Container               |
---------------------------------

---

# 🧱 STEP 1: Create Shared Docker Network

Run this only once on the server:

```bash
docker network create dd_network
```

Both frontend and backend will use this shared external network.

---

# 📦 FRONTEND SETUP (Angular - Development Mode)

# 📄 Frontend Dockerfile
      frontend docker-compose.yaml
      Inside frontend repository:

```bash
docker compose up --build -d
```



# ▶️ STEP 2: Start Backend
# 📄 backend Dockerfile
     backend docker-compose.yaml

Inside backend repository:


```bash
docker compose up --build -d
```

---




# 🌐 NGINX SETUP (Host Machine)

Edit:

```
/etc/nginx/sites-available/default
```

Replace with:

```nginx
server {
    listen 80;

    server_name _;  # underscore is a catch-all when no domain is used

    location / {
        proxy_pass http://127.0.0.1:8081;
        proxy_http_version 1.1;                 # required for WebSockets
        proxy_set_header Upgrade $http_upgrade; # handle WebSocket upgrade
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Backend (served on /api/)
    location /api/ {
        proxy_pass http://127.0.0.1:8082;  # backend
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Then restart nginx:

```bash
sudo nginx -t
sudo systemctl restart nginx
```





