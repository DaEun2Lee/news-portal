# News Portal (Docker Deployment)

## 📌 Original Source

Original project repository:

https://github.com/sahrulromadi/laravel-news-portal

---

## 🐳 Docker-Based Deployment Guide

This guide explains how to deploy the Laravel News Portal project using Docker while keeping the current structure (including `php artisan serve`).

---

# 📂 Project Structure

```
news-portal-backup/
├── docker-compose.yml
├── Dockerfile
├── .env
├── db-backup/
│   └── news_portal_backup.sql
├── storage/
└── source/   (cloned laravel project)
```

---

# 1️⃣ Clone Original Source

```bash
git clone https://github.com/sahrulromadi/laravel-news-portal.git source
cd source
```

---

# 2️⃣ Create Dockerfile

Create a file named `Dockerfile` in the root directory:

```Dockerfile
FROM php:8.1-cli

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git curl unzip libpng-dev libonig-dev libxml2-dev zip

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY source/ /var/www

RUN composer install

EXPOSE 8000

CMD php artisan serve --host=0.0.0.0 --port=8000
```

---

# 3️⃣ Create docker-compose.yml

```yaml
version: '3.8'

services:
  app:
    build: .
    container_name: news_portal_app
    ports:
      - "8224:8000"
    volumes:
      - ./source:/var/www
      - ./storage:/var/www/storage
    depends_on:
      - db
    networks:
      - newsnet

  db:
    image: mysql:8.0
    container_name: news_portal_db
    restart: always
    environment:
      MYSQL_DATABASE: news_portal
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: laravel
      MYSQL_PASSWORD: laravel
    ports:
      - "3307:3306"
    volumes:
      - db_data:/var/lib/mysql
      - ./db-backup:/docker-entrypoint-initdb.d
    networks:
      - newsnet

volumes:
  db_data:

networks:
  newsnet:
```

---

# 4️⃣ Configure .env

Update `.env` file inside `source/`:

```env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=news_portal
DB_USERNAME=laravel
DB_PASSWORD=laravel
```

---

# 5️⃣ Prepare Storage Directory

Create storage folder:

```bash
mkdir -p storage
```

Set permission (Linux):

```bash
chmod -R 777 storage
```

Then inside container:

```bash
docker compose exec app php artisan storage:link
```

---

# 6️⃣ Database Import (Optional if backup exists)

Place your SQL backup file in:

```
db-backup/news_portal_backup.sql
```

MySQL container will automatically import it during first startup.

---

# 7️⃣ Run the Application

```bash
docker compose up -d --build
```

Access via browser:

```
http://localhost:8224
```

If deployed on server:

```
http://SERVER_IP:8224
```

---

# 📦 Backup Structure Example

```
news-portal-backup/
├── docker-compose.yml
├── Dockerfile
├── .env
├── db-backup/
│   └── news_portal_backup.sql
└── storage/
```

---

# ⚠ Notes

- This deployment keeps `php artisan serve`.
- This is suitable for development or internal deployment.
- For production environments, consider using Nginx + PHP-FPM instead of `artisan serve`.

---

# ✅ Quick Start Summary

```bash
docker compose up -d --build
```

Open browser → `http://localhost:8224`

---

# 🎉 Done

Your Laravel News Portal is now running inside Docker.
