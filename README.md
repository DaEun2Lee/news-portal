📰 Laravel News Portal (Docker Deployment Version)

Original Source: https://github.com/sahrulromadi/laravel-news-portal

This repository packages the original project for Docker-based deployment with DB backup support.

📦 Project Structure
news-portal-backup/
├── docker-compose.yml
├── .env
├── Caddyfile
├── db-backup/
│   └── news_portal_backup.sql
└── storage/
🐳 Requirements

Docker

Docker Compose

Linux / WSL / macOS

Available Ports:

HTTP → 8224

HTTPS → 8444

MySQL → 3307

🚀 Installation & Run
1️⃣ Clone Project
git clone <your-repository-url>
cd news-portal-backup
2️⃣ Start Containers
sudo docker compose up -d --build

Check status:

sudo docker ps
3️⃣ Restore Database Backup

Import the included SQL backup file:

sudo docker exec -i laravel_news_db \
  mysql -u root -proot news_portal < db-backup/news_portal_backup.sql

Verify:

sudo docker exec -it laravel_news_db mysql -u root -proot
SHOW DATABASES;
USE news_portal;
SHOW TABLES;
4️⃣ Laravel Initialization

Enter Laravel container:

sudo docker exec -it news_center_app bash

Clear caches:

php artisan config:clear
php artisan cache:clear
php artisan route:clear
php artisan view:clear

If sessions/cache tables are required:

php artisan session:table
php artisan cache:table
php artisan migrate
🌐 Access
HTTP
http://SERVER_IP:8224

Example:

http://10.20.16.66:8224
HTTPS (Self-Signed)
https://news-portal.local:8444

Browser may show a security warning due to self-signed certificate.

⚙️ Important .env Settings
APP_ENV=local
APP_DEBUG=true
APP_URL=http://10.20.16.66:8224

DB_CONNECTION=mysql
DB_HOST=laravel_news_db
DB_PORT=3306
DB_DATABASE=news_portal
DB_USERNAME=newsuser
DB_PASSWORD=newspass

SESSION_DRIVER=file
CACHE_STORE=file
QUEUE_CONNECTION=sync
🧱 Architecture
Client
   ↓
Caddy (Reverse Proxy + HTTPS + HTTP/3)
   ↓
Laravel (artisan serve)
   ↓
MySQL (Docker Volume)

Caddy → Reverse proxy, HTTPS, HTTP/3

Laravel → php artisan serve

MySQL → Persistent Docker volume storage

💾 Docker Volume

Check volumes:

sudo docker volume ls

MySQL data volume:

laravel-news-portal_laravel_news_db_data
🛑 Stop Containers
sudo docker compose down

Remove volumes:

sudo docker compose down -v
📌 Notes

Set APP_DEBUG=false in production.

Use a real TLS certificate for production.

artisan serve is development-oriented (not recommended for high traffic).

For production: consider nginx + php-fpm architecture.

🎯 Purpose of This Setup

Docker-based reproducible environment

WAN optimization experiments

HTTP/3 (QUIC) testing

Reverse proxy testing

📄 License

This project follows the original repository’s license.
See original source for details:

https://github.com/sahrulromadi/laravel-news-portal
