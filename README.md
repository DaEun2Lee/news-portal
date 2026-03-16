# News Center

**News Center** is a simple, dynamic news web portal that allows content to be customized to your preference. This project enables users to add, manage, and display news in an easy and efficient manner.

## Features

-   **News Management:** Easily add, edit, and delete news.
-   **Responsive Design:** A responsive layout that works well on various devices.
-   **News CRUD:** Create, Read, Update, and Delete operations for news.
-   **Admin Panel:** An admin panel for managing news and users.

## Credits

-   Home template: [Newsers](https://themewagon.com/themes/newsers/)
-   Admin template: [Kaiadmin](https://themewagon.com/themes/kaiadmin/)

---

## Screenshot

![Screenshot 2024-09-15 003150](https://github.com/user-attachments/assets/b4c431ee-a0b6-4217-b1b4-1179e4de5363)

![Screenshot 2024-09-15 003326](https://github.com/user-attachments/assets/ffd1ab60-24de-4ed3-beaa-52bb444977c4)

![Screenshot 2024-09-15 003304](https://github.com/user-attachments/assets/222bde07-dcf2-4ce0-a222-b8b536e2adf1)

---

## Installation Steps

Follow these steps to install the project on your local machine:

### 1. Clone the Repository

Clone this repository to your local machine:

```bash
git clone "https://github.com/sahrulromadi/News-Center.git"
```

### 2. Navigate to the Project Directory

```bash
cd News-Center
```

### 3. Install Composer Dependencies

```bash
composer install
```

### 4. Copy Configuration File

```bash
cp .env.example .env
```

### 5. Configure the .env File

Edit the .env file to match your database configuration. Example:

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database_name
DB_USERNAME=your_database_user
DB_PASSWORD=your_database_password
```

### 6. Generate Application Key

```bash
php artisan key:generate
```

### 7. Migrate and Seed the Database

```bash
php artisan migrate
php artisan db:seed
```

### 8. Start the Local Server

```bash
php artisan serve
```

---

## Accessing the Admin Panel

To access the admin panel, follow these steps:

1. Open your browser and navigate to:

```bash
http://127.0.0.1:8000/login
```

2. Alternatively, you can type this on the home page:

```bash
admin
```

3. Use the following default admin credentials to log in:

-   **Email:** `admin@gmail.com`
-   **Password:** `admin123`
