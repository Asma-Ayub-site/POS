# 🧾 POS Web Application — PHP & MySQL

![PHP](https://img.shields.io/badge/PHP-777BB4?style=flat\&logo=php\&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat\&logo=mysql\&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat\&logo=javascript\&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

A lightweight, self-hosted **Point of Sale (POS) system** built with PHP, MySQL, and vanilla JavaScript — designed for small restaurants and fast-food outlets. It handles menu/stock management, billing, table & waiter tracking, and printable sale receipts, all running locally on XAMPP with no external dependencies.

## 📑 Table of Contents

* [Features](#-features)
* [Screenshots](#-screenshots)
* [Tech Stack](#-tech-stack)
* [Project Structure](#-project-structure)
* [Database Schema](#-database-schema)
* [Getting Started](#-getting-started)
* [Default Login](#-default-login)
* [API / Endpoints Overview](#-api--endpoints-overview)
* [Troubleshooting](#-troubleshooting)
* [Security Notes](#-security-notes)
* [Roadmap](#-roadmap)
* [Contributing](#-contributing)
* [License](#-license)


## ✨ Features

| Category                        | Details |
| ------------------------------  | --------------------------------------------------------------------------------------------------- |
| 🔐 **Authentication**           | Login & registration with `password_hash()` / `password_verify()` bcrypt hashing and PHP session management |
| 📦 **Stock / Menu Management**  | Add, edit, and delete menu items — category, name, price, and image upload  |
| 🧾 **Billing System**           | Category-wise menu browsing, add items to a live bill, automatic total calculation |
| 🍽️ **Table & Waiter Tracking**  | Bills grouped and viewable by table number and waiter name |
| 📊 **Bill Records & Reports**   | Search bills by token number, add/remove items from an existing bill, view total revenue and order count    |
| 🖨️ **Printable Receipts**       | Auto-generated, print-ready sale receipt with discount % and payment method |
| 📱 **Responsive UI**             | Usable on both desktop and mobile screens |


## 📷 Screenshots

> Add screenshots of your app here once deployed, for example:

| Login                           | Dashboard                               | Billing                             |
| ------------------------------- | --------------------------------------- | ----------------------------------- |
| ![Login](screenshots/login.png) | ![Dashboard](screenshots/dashboard.png) | ![Billing](screenshots/billing.png) |


## 🛠️ Tech Stack

* **Backend:** PHP (`mysqli`, prepared statements)
* **Database:** MySQL / MariaDB
* **Frontend:** HTML, CSS, JavaScript (jQuery for AJAX calls)
* **Local Server:** XAMPP (Apache + MySQL + PHP)
* **Data Storage:** MySQL for menu/stock and user accounts; bills stored as JSON in `bills_record.json`


## 📂 Project Structure

text
pos3/
├── login.php                 # Login & registration
├── logout.php                # Logout handler
├── dashboard.html            # Admin dashboard
├── billing.html              # Billing / POS screen
├── billing.js                # Billing JavaScript
├── billing.css               # Billing styles
├── edit.php                  # Stock management
├── edit_item.php             # Edit stock item
├── get_categories.php        # Fetch distinct menu categories
├── get_items.php             # Fetch menu items
├── insert_stock.php          # Stock table listing (AJAX)
├── add_item.php              # Add stock item (legacy endpoint)
├── update_products.php       # Update stock item (AJAX)
├── save_bill.php             # Save a new bill
├── view_bills.php            # View / search / manage bills
├── table_cover.php           # Table & waiter records
├── index.html                # Standalone insert stock form
├── script.js                 # Standalone form JavaScript
├── styles.css                # Shared styles
├── uploads/                  # Uploaded menu item images
├── bills_record.json         # Bill/order storage (JSON)
├── logo.png                  # Restaurant logo
└── pos.sql                   # Database schema + seed data


## 🗄️ Database Schema

The application uses a MySQL database named `pos` with two main tables:

| Table   | Columns                                         | Purpose                                    |
| ------- | ----------------------------------------------- | ------------------------------------------ |
| `stock` | `id`, `category`, `name`, `price`, `image_path` | Menu items displayed on the billing screen |
| `user`  | `id`, `username`, `email`, `password`           | Login accounts with bcrypt password hashes |

> ℹ️ **Note:** Orders and bills are not stored in MySQL. They are saved in `bills_record.json` in the project root.

## 🚀 Getting Started

### Requirements

* [XAMPP](https://www.apachefriends.org/)
* PHP 8.1+
* MySQL / MariaDB
* A modern web browser

### Installation

#### 1. Clone the Repository

Clone the repository into your XAMPP `htdocs` folder:

bash
git clone https://github.com/<your-username>/<your-repo>.git

#### 2. Start XAMPP

Open the **XAMPP Control Panel** and start:

* Apache
* MySQL

#### 3. Create the Database

Open:

text
http://localhost/phpmyadmin

Then:

1. Create a new database named `pos`.
2. Open the **Import** tab.
3. Select the `pos.sql` file.
4. Click **Go**.

#### 4. Verify Database Connection

Check the database connection settings in PHP files such as `login.php`, `edit.php`, `save_bill.php`, and other database-related files.

Default configuration:

php
$servername = "localhost";
$username   = "root";
$password   = "";
$dbname     = "pos";


> ⚠️ Make sure the `$dbname` value matches the database name created in phpMyAdmin.

#### 5. Check Required Writable Files/Folders

Make sure the web server can write to:

text
uploads/
bills_record.json

The `uploads/` folder is required for menu item images, while `bills_record.json` is required for saving bills.

#### 6. Open the Application

Open the following URL in your browser:

text
http://localhost/<project-folder>/login.php
## 🔑 Default Login

The default account is seeded through `pos.sql`.

| Username | Password   |
| -------- | ---------- |
| `admin`  | `admin123` |

> You can also register a new account directly from the login page.

## 🔌 API / Endpoints Overview

| Endpoint                     | Method      | Purpose                                          |
| ---------------------------- | ----------- | ------------------------------------------------ |
| `login.php`                  | POST        | Login and registration                           |
| `logout.php`                 | GET         | Destroy the current session                      |
| `get_categories.php`         | GET         | List distinct menu categories                    |
| `get_items.php`              | GET         | List menu items, optionally filtered by category |
| `edit.php` / `edit_item.php` | GET/POST    | Add, edit, and delete stock items                |
| `update_products.php`        | POST (JSON) | Update a stock item through AJAX                 |
| `save_bill.php`              | POST        | Save a new bill to `bills_record.json`           |
| `view_bills.php`             | GET/POST    | View, search, add to, or delete bills            |
| `table_cover.php`            | GET/POST    | Manage table and waiter grouped records          |

## 🛠️ Troubleshooting

| Problem                                                     | Cause                                                                                                                                                          | Fix                                                                                                                                                              |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Unknown database 'pos_db'`                                 | The `$dbname` value in the PHP files does not match the actual MySQL database name.                                                                            | Check the database name in phpMyAdmin and make sure the `$dbname` variable in every PHP file matches it exactly.                                                 |
| `Duplicate entry 'admin' for key 'username'` (Fatal Error)  | The username/email already exists in the database, and PHP 8.1+ throws an uncaught `mysqli_sql_exception` when another record with the same value is inserted. | Wrap the `INSERT` query in a `try/catch` block and display a friendly message such as **"Username already taken"** instead of allowing the application to crash. |
| Registration works, but login says **"Incorrect password"** | The `password` column is too short, for example `VARCHAR(50)`, so the bcrypt hash is truncated when stored.                                                    | Change the `password` column to `VARCHAR(255)` in phpMyAdmin, then register the user again so a complete password hash is stored.                                |
| Images are not showing after upload                         | The `uploads/` folder is missing or does not have the required write permissions.                                                                              | Create the `uploads/` folder manually and make sure the web server has permission to write files to it.                                                          |

## Recommended Troubleshooting Order

1. Check the database name.
2. Confirm that all required tables exist.
3. Check that the `password` column is `VARCHAR(255)`.
4. Fix duplicate username/email handling.
5. Create the `uploads/` folder if it does not exist.
6. Check folder and file permissions.
7. Test the complete application flow:

 text
Register → Login → Add Menu Item → Upload Image → Create Bill → Save Bill → View Receipt

## 🔒 Security Notes

1. Passwords are hashed using `password_hash()` with bcrypt and are never stored as plain text.
2. Most database queries use **prepared statements** to help prevent SQL injection.
3. The project is designed primarily for **local/learning use with XAMPP**.

** Before Public Deployment**

The following security improvements should be implemented before deploying the application publicly:

* Move database credentials to environment variables instead of hardcoding `root` with an empty password.
* Enforce HTTPS.
* Add CSRF protection to forms and state-changing requests.
* Restrict uploaded file types and file sizes server-side.
* Validate and sanitize uploaded file names.
* Add proper authentication and authorization checks.
* Disable unnecessary PHP error output in production.

## 🗺️ Roadmap

* [ ] Move bill storage from JSON to a proper MySQL table.
* [ ] Add role-based access control for admin, waiter, and staff accounts.
* [ ] Add a sales analytics dashboard with daily, weekly, and monthly reports.
* [ ] Add multi-branch support.
* [ ] Improve validation and error handling.
* [ ] Add stronger file-upload security.
* [ ] Improve reporting and receipt management.

## 🤝 Contributing

Contributions are welcome!
To contribute:
1. Fork the repository.
2. Create a feature branch:
bash
git checkout -b feature/your-feature
3. Commit your changes:
bash
git commit -m "Add your feature"
4. Push the branch:
bash
git push origin feature/your-feature
5. Open a Pull Request.

## 📄 License

This project is open-source and available under the **MIT License** for personal or educational use.

See the [LICENSE](LICENSE) file for more information.
