# 🚀 LEMP Stack Project (Ubuntu 20.04)

## 📌 Introduction

The LEMP stack is a widely used web development stack consisting of **Linux, Nginx (Engine-X), MySQL, and PHP**. It is designed to serve dynamic web applications efficiently and is commonly used in production environments due to its high performance and scalability.

In this project, a complete LEMP stack environment was built on an Ubuntu 20.04 server using a Vagrant virtual machine. The setup includes the installation and configuration of Nginx as the web server, MySQL as the database system, and PHP-FPM for processing dynamic PHP scripts.

The project also demonstrates how these components interact together to serve dynamic web pages and connect to a database through PHP, resulting in a fully functional backend web application environment.

---

##  Project Overview

This project demonstrates the installation and configuration of a full LEMP stack on an Ubuntu server (Vagrant environment). It includes:

- Linux (Ubuntu 20.04)
- Nginx Web Server
- MySQL Database
- PHP-FPM for dynamic processing

It also includes a working PHP–MySQL integration test application.

---

## ⚙️ Tech Stack

- **Operating System:** Ubuntu 20.04 (Vagrant VM)
- **Web Server:** Nginx
- **Database:** MySQL
- **Backend Language:** PHP 7.2 / PHP-FPM

---

## 📦 Installation Steps Summary

### 1. Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

Enable firewall
```
sudo ufw allow 'Nginx HTTP'
```

### 2. Install MySQL
```
sudo apt install mysql-server -y
sudo mysql_secure_installation
```
### 3. Install PHP and PHP-FPM
```
sudo apt install php-fpm php-mysql -y
```
### 4. Configure Nginx for PHP

Edit default config:
```
sudo nano /etc/nginx/sites-available/default
```

Enable PHP support:
```
index index.php index.html index.htm;

location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
}
```

Reload Nginx:

```
sudo nginx -t
sudo systemctl reload nginx
```

### Project Test Files
#### PHP Info Test
```
<?php
phpinfo();
?>
```

Access:

```
http://localhost:8080/info.php
```
### MySQL + PHP Integration (Todo App)
#### Database Setup
```
CREATE DATABASE example_database;

CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'Th3S@ints216!';

GRANT ALL ON example_database.* TO 'example_user'@'%';
```
#### Table Setup
```
USE example_database;

CREATE TABLE todo_list (
    item_id INT AUTO_INCREMENT,
    content VARCHAR(255),
    PRIMARY KEY(item_id)
);

INSERT INTO todo_list (content) VALUES ('My first item');
INSERT INTO todo_list (content) VALUES ('My second item');
```
#### PHP Script (todo.php)
```
<?php
$pdo = new PDO(
    "mysql:host=localhost;dbname=example_database",
    "example_user",
    "password"
);

$stmt = $pdo->query("SELECT * FROM todo_list");

echo "<h1>Todo List</h1>";
echo "<ul>";

while ($row = $stmt->fetch()) {
    echo "<li>" . $row['content'] . "</li>";
}

echo "</ul>";
?>
```
##### Access:
```
http://localhost:8080/todo.php
```
### Features
- Fully working LEMP stack
- PHP execution via Nginx + PHP-FPM
- MySQL database integration
- Dynamic PHP database query display
- Vagrant-based local development environment
### Cleanup (Security)

Remove test files:
```
sudo rm /var/www/html/info.php
sudo rm /var/www/html/todo.php
```
### Learning Outcome

#### This project demonstrates:

- Web server configuration (Nginx)
- Database setup (MySQL)
- Server-side scripting (PHP)
- Backend database integration
- Linux server management basics


<img width="2242" height="600" alt="image" src="https://github.com/user-attachments/assets/408fc018-49b2-40d6-a6ef-c999d63261b6" />

<img width="2528" height="970" alt="image" src="https://github.com/user-attachments/assets/433732a1-3587-47ef-a1c0-7d46c43298cc" />

<img width="2370" height="490" alt="image" src="https://github.com/user-attachments/assets/496c7085-3f27-4c5d-9db8-346101426bbe" />

<img width="1446" height="226" alt="image" src="https://github.com/user-attachments/assets/76ae7707-e010-4439-9d9d-b3d193faede0" />

<img width="1968" height="1074" alt="image" src="https://github.com/user-attachments/assets/f941d65e-9461-4e16-887b-6faaae7324fb" />

<img width="2078" height="1082" alt="image" src="https://github.com/user-attachments/assets/2af5d047-dd52-43b2-be92-85eea2caacab" />

<img width="1028" height="1272" alt="image" src="https://github.com/user-attachments/assets/4b9d0492-2c43-4a5c-8fbe-7205ea1db8ce" />





