# Manual MVC in PHP: PDO, SQL Injection and MVC from Scratch

Source code for the **Manual MVC in PHP** video series on the [StudyVerse YouTube channel](https://www.youtube.com/@studyverse8981).
Built step by step in plain PHP, with no framework, by **Dr. Muhammad Faisal Abrar**.

## What's inside

| Folder | What it shows |
|---|---|
| `pdo-demos/` | The same "add a student" page written with **mysqli**, the **pg_\*** functions and **PDO**, plus a live **SQL injection** attack and its fix |
| `student-manager/` | A small **Student Manager** app built with a custom MVC structure: model, controller, router and views |

## Requirements

- [XAMPP](https://www.apachefriends.org/download.html) (Apache, PHP and MySQL/MariaDB)
- [VS Code](https://code.visualstudio.com/download) or any code editor
- PostgreSQL is optional (only for `2_pgsql.php` and the PostgreSQL option in `3_pdo.php`)

## 1. PDO demos (`pdo-demos/`)

1. Copy the `pdo-demos` folder into `C:\xampp\htdocs\`.
2. Start **Apache** and **MySQL** in the XAMPP Control Panel.
3. Open phpMyAdmin, go to the **SQL** tab and run `setup_mysql.sql`. It creates the `pdo_demo` database and the `students` table.
4. Open the steps in your browser:

| File | URL | Shows |
|---|---|---|
| `1_mysqli.php` | `localhost/pdo-demos/1_mysqli.php` | mysqli: works only with MySQL |
| `2_pgsql.php` | `localhost/pdo-demos/2_pgsql.php` | The same page rewritten for PostgreSQL: almost every database line changes |
| `3_pdo.php` | `localhost/pdo-demos/3_pdo.php` | PDO: switch databases by changing one line (`$use = "mysql"` or `"pgsql"`) |
| `4_sql_injection.php` | `localhost/pdo-demos/4_sql_injection.php` | A live SQL injection attack, and how prepared statements stop it |

**PostgreSQL (optional):** create a database called `pdo_demo` in pgAdmin, run `setup_pgsql.sql` on it, and replace `your_password` in `2_pgsql.php` and `3_pdo.php` with your PostgreSQL password.

**Try the attack in step 4:** type `' OR '1'='1` as the email and click **Search (unsafe)**: every student is returned. Click **Search (safe)** with the same text: nothing is returned, because the prepared statement treats it as plain data.

> Run the SQL injection demo only on your own local database, never on a real website.

## 2. Student Manager in custom MVC (`student-manager/`)

```
student-manager/
├── config/database.php           Database connection (PDO)
├── models/Model.php              Base model: gives every model $this->db
├── models/students.php           Student model: all() and create()
├── Controllers/StudentController.php   index(), create(), store()
├── Views/Layout/header.php       Shared header and menu
├── Views/Layout/footer.php       Shared footer
├── Views/Student/index.php       List of students
├── Views/Student/create.php      Add-student form
└── public/index.php              Front controller and router
```

1. Copy the `student-manager` folder into `C:\xampp\htdocs\`.
2. In phpMyAdmin, create a database called `mvctuts` with a `students` table:

```sql
CREATE DATABASE mvctuts;
USE mvctuts;
CREATE TABLE students (
    id    INT AUTO_INCREMENT PRIMARY KEY,
    name  VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL
);
```

3. Open `localhost/student-manager/public/` in your browser.

**How a request flows:** browser → `public/index.php` (router) → `StudentController` → `Student` model → database, and back through the view.

## Video series

1. Setting Up VS Code for PHP
2. What Are Model, View and Controller?
3. Database, Connection and Model
4. The Controller and the Front Door
5. A Simple Router
6. Layout, Views and Saving with a Form
7. PDO in PHP

## Security note

The database settings use XAMPP's defaults (`root` with an empty password), which is fine on your own computer. 
