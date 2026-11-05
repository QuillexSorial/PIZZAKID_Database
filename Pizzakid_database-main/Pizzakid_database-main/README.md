# 🍕 PizzaKid POS Database System

---

### *Streamlining Orders. Automating Inventory. Powering Pabayo CDO.*

<p align="left">
  <img src="https://img.shields.io/badge/DATABASE-MYSQL-00758F?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/TOOL-PHPMYADMIN-D16100?style=for-the-badge&logo=phpmyadmin&logoColor=white" alt="phpMyAdmin" />
  <img src="https://img.shields.io/badge/ENVIRONMENT-XAMPP-F37C20?style=for-the-badge&logo=xampp&logoColor=white" alt="XAMPP" />
</p>

Welcome to the **PizzaKid POS Database Repository**! 👋

This repository contains the complete MySQL relational database schema, recipe triggers, and 50-transaction sample seed data for the **PizzaKid Point of Sale (POS) System** (Pabayo St. Branch, Cagayan de Oro City). It is engineered to handle high-throughput cashier ordering, automated ingredient inventory deduction, custom menu modifier pricing, and kitchen display prep workflows.

The database supports 20 core relational tables covering multi-role user authentication, itemized transactions, split payments, recipe-based stock deduction, KDS updates, terminal synchronization, and operational audit logs.

---

## 📌 Table of Contents

* [🎯 Project Overview](#-project-overview)
* [✨ Database Features](#-database-features)
* [⚙️ Automated Triggers and Routines](#%EF%B8%8F-automated-triggers-and-routines)
* [🛠️ Technologies Used](#%EF%B8%8F-technologies-used)
* [🚀 Getting Started](#-getting-started)
* [💻 Sample SQL Queries](#-sample-sql-queries)
* [🔒 Project Notes](#-project-notes)
* [⭐ Support the Project](#-support-the-project)

---

## 🎯 Project Overview

The **PizzaKid POS Database (`pizza_db`)** serves as the data storage foundation of a Point of Sale and Inventory Management System tailored for PizzaKid (Pabayo St. Branch, Cagayan de Oro City).

It provides an organized 20-table relational database structure for storing, retrieving, and maintaining records involved in daily store transactions, kitchen prep workflows, and ingredient inventory management.

It also includes automated database triggers, relational constraints, and indexed queries that support common store operations, such as recipe-based stock deductions, dynamic menu modifier pricing, cashier shift tracking, and multi-terminal synchronization.

**The goal is simple: Streamline order processing, automate inventory tracking, and make daily store operations easier to manage.**

---

## ✨ Database Features

| Feature | Description |
| :--- | :--- |
| 👤 **User & Role Management** | Stores manager PINs, cashier shift states, and kitchen staff station assignments. |
| 🍕 **Menu Catalog** | Stores pizza categories, items, descriptions, pricing, and item availability. |
| 🧀 **Modifier Engine** | Handles crust options, extra toppings, selection limits (`min_selection`, `max_selection`), and add-on pricing. |
| 📦 **Inventory Control** | Tracks raw ingredient stock levels, minimum reorder thresholds, and unit measurements. |
| 📖 **Recipe Mapping** | Links menu items directly to ingredients for automatic recipe-based inventory deduction. |
| 🛒 **Order Lifecycle** | Manages Dine-In, Takeout, and Delivery transactions and itemized line-item totals. |
| 💳 **Payment Records** | Tracks split payments, payment methods (Cash, GCash, Maya, Card), and processing status. |
| 🍳 **Kitchen Display System** | Monitors station-specific prep progress from order receipt to completion. |
| 🔄 **POS Sync Logging** | Maintains multi-terminal sync status and handles transaction transmission logs. |
| 🛡️ **Audit & Notifications** | Records user action logs, low-stock reorder alerts, and manager authorization overrides. |





---

## 🛠️ Technologies Used

* **MySQL** – Relational database management system.
* **phpMyAdmin** – Database administration and management.
* **XAMPP** – Local development environment.
* **SQL** – Database queries, automated inventory triggers, and relational schemas.
* **Draw.io** – ERD schema modeling and database relationship mapping.

---

## 🚀 Getting Started

Ready to explore the database? Follow these steps!

### 1. Prepare the Environment

* Install [XAMPP](https://www.apachefriends.org/).
* Open XAMPP Control Panel.
* Start **Apache** and **MySQL**.

### 2. Open phpMyAdmin

Visit:

```text
http://localhost/phpmyadmin
```

### 3. Create the Database

Create a new database named:

```sql
CREATE DATABASE pizza_db;
```

### 4. Import the SQL Files

If you are using separate SQL files:

1. Select the `pizza_db` database on the left sidebar.
2. Click the **Import** tab in the top navigation bar.
3. Import `schema.sql` first.
4. Import `sample_data.sql` next.
5. Import `triggers.sql` last.
6. Wait for each import process to finish.

**Alternative:** You can import `pizza_db.sql` directly if it already contains the complete database structure and sample records.

🎉 **Your database is now ready to explore!**

---

## 💻 Sample SQL Queries

### 1. Daily Sales Summary by Payment Method
```sql
SELECT 
    payment_method, 
    COUNT(payment_id) AS total_transactions, 
    SUM(amount_paid) AS total_revenue
FROM payments
WHERE payment_status = 'Completed'
GROUP BY payment_method;
```

### 2. Low Inventory Warning Report
```sql
SELECT 
    item_name, 
    quantity_in_stock, 
    minimum_stock, 
    unit
FROM inventory_items
WHERE quantity_in_stock <= minimum_stock;
```

### 3. Top Selling PizzaKid Menu Items
```sql
SELECT 
    m.item_name, 
    SUM(oi.quantity) AS total_sold, 
    SUM(oi.subtotal) AS gross_sales
FROM order_items oi
JOIN menu_items m ON oi.menu_item_id = m.menu_item_id
GROUP BY m.menu_item_id
ORDER BY total_sold DESC;
```

---

## 🔒 Project Notes

* **Foreign Key Checks**: Foreign Key Integrity Constraints are enforced across all 20 tables.
* **Data Resets**: When clearing or re-seeding table contents, use `DELETE FROM table_name;` rather than `TRUNCATE TABLE table_name;` to prevent MySQL Error #1701 on foreign key referenced tables.
* **Storage Engine**: All tables use the `InnoDB` engine with `utf8mb4_general_ci` collation.

---

## ⭐ Support the Project

If this database schema and seed script helped you build or understand your Point of Sale system, please consider leaving a ⭐ on this repository!
