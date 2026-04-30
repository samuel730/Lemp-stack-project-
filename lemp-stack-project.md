#  LEMP Stack Project (Ubuntu 20.04)

## Introduction

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

##  Tech Stack

- **Operating System:** Ubuntu 20.04 (Vagrant VM)
- **Web Server:** Nginx
- **Database:** MySQL
- **Backend Language:** PHP 7.2 / PHP-FPM

---

##  Installation Steps Summary

### 1. Install Nginx

```bash
sudo apt update
sudo apt install nginx -y
```
<img width="2551" height="1345" alt="Screenshot 2026-04-05 190134" src="https://github.com/user-attachments/assets/976f489f-3d60-44e3-adad-dca946e6ef57" />
<img width="1553" height="340" alt="Screenshot 2026-04-05 190119" src="https://github.com/user-attachments/assets/d00f4173-48c7-4aba-81e9-ac424af55952" />

Enable firewall
```
sudo ufw allow 'Nginx HTTP'
```
<img width="1020" height="124" alt="Screenshot 2026-04-05 190230" src="https://github.com/user-attachments/assets/39f3b6a8-56ee-4037-a34b-0ced11201c1c" />

### 2. Install MySQL
```
sudo apt install mysql-server -y
sudo mysql_secure_installation
```
<img width="2369" height="490" alt="Screenshot 2026-04-23 124142" src="https://github.com/user-attachments/assets/a7b663c8-3ca9-4827-983c-422d1d199947" />

### 3. Install PHP and PHP-FPM
```
sudo apt install php-fpm php-mysql -y
```
<img width="1446" height="225" alt="Screenshot 2026-04-23 124209" src="https://github.com/user-attachments/assets/938ab2c9-788c-422d-8086-e0df6b6706c9" />

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

<img width="2528" height="969" alt="Screenshot 2026-04-23 124104" src="https://github.com/user-attachments/assets/3465e4ba-2bf6-43ca-a787-faa2011d765b" />
<img width="2369" height="490" alt="Screenshot 2026-04-23 124142" src="https://github.com/user-attachments/assets/ceed7c15-9a99-4633-9721-8fefeee9c99a" />
<img width="1446" height="225" alt="Screenshot 2026-04-23 124209" src="https://github.com/user-attachments/assets/0978245c-63bd-464c-9ed9-581887042227" />
<img width="1967" height="1074" alt="Screenshot 2026-04-23 124247" src="https://github.com/user-attachments/assets/f85aa805-e1e0-4c24-9d62-52bbe46a60b9" />
<img width="2078" height="1081" alt="Screenshot 2026-04-23 124322" src="https://github.com/user-attachments/assets/d5cf9333-52a5-4350-868b-5e5e6ba6e206" />
<img width="1028" height="1272" alt="Screenshot 2026-04-23 124354" src="https://github.com/user-attachments/assets/4b2b05f6-779d-4b91-9606-e53295de718f" />


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





