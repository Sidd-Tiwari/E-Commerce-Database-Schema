# Pharmacy Management System - Database Schema

## 📌 Overview
This project contains the **database schema** for a Pharmacy Management System. It is designed to efficiently handle users, medicines, inventory, orders, payments, and suppliers while ensuring optimized query performance.

---

## 🏗 Database Schema
The database follows **Third Normal Form (3NF)** and includes the following tables:

1. **users** - Stores user details (Admin, Pharmacist, Customers)
2. **medicines** - Stores medicine details with stock tracking
3. **inventory** - Manages supplier and stock details
4. **orders** - Stores customer orders
5. **order_items** - Manages individual medicines within orders
6. **payments** - Tracks payments for orders
7. **suppliers** - Stores supplier information

---

## 🛠 Installation

### **MySQL Deployment**
1. **Create the database:**
   ```sql
   CREATE DATABASE pharmacy_db;
   USE pharmacy_db;
   ```
2. **Run the schema script:**
   ```bash
   mysql -u root -p pharmacy_db < pharmacy_schema.sql
   ```

### **PostgreSQL Deployment**
1. **Create the database:**
   ```sql
   CREATE DATABASE pharmacy_db;
   ```
2. **Run the schema script:**
   ```bash
   psql -U postgres -d pharmacy_db -f pharmacy_schema.sql
   ```

---

## 🚀 Query Optimization

### **Indexes for Faster Queries**
```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user ON orders(user_id);
CREATE INDEX idx_medicine_name ON medicines(name);
```

### **Retrieve Top-Selling Medicines Per Region**
```sql
SELECT m.name, COUNT(oi.id) AS total_sold, u.region
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
JOIN medicines m ON oi.medicine_id = m.id
JOIN users u ON o.user_id = u.id
GROUP BY m.name, u.region
ORDER BY total_sold DESC
LIMIT 10;
```

---

## 🔄 Automated Backup
Create a **backup script (`backup.sh`)**:
```bash
#!/bin/bash
mysqldump -u root -p pharmacy_db > backup.sql
git add backup.sql
git commit -m "Automated backup - $(date)"
git push origin main
```
Schedule it using a cron job:
```bash
crontab -e
```
Add this line to run daily at midnight:
```bash
0 0 * * * /path/to/backup.sh
```

---

## 🔹 Contributing
1. Fork the repository.
2. Create a new branch (`feature-new-table`).
3. Commit your changes.
4. Push to GitHub.
5. Submit a pull request.

---

## 📜 License
This project is licensed under the **MIT License**.

