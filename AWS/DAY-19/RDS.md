# 📘 AWS RDS 

---

## What is a Database?

A **database** is a place to store, organize, and manage data.

**Examples:**
- WhatsApp stores your messages in a database.
- Banks store customer information in a database.

---

##  Types of Databases

1. **Relational Database** – stores data in **tables**
   - Examples: MySQL, PostgreSQL, Oracle, SQL Server
   - Uses **SQL (Structured Query Language)**

2. **Non-Relational (NoSQL)** – used for unstructured data  
   - Examples: MongoDB, DynamoDB

---

##  What is AWS?

**AWS (Amazon Web Services)** is a cloud platform that provides services like servers, databases, storage, and more over the internet.

---

##  What is AWS RDS?

**Amazon RDS (Relational Database Service)** is a managed service that helps you run a **relational database** in the cloud without worrying about installation, patching, backups, etc.

> ✅ AWS handles the heavy lifting like maintenance, backups, and updates.

---

## 🎯 Why Use AWS RDS?

- ✅ Easy to set up
- ✅ Automatic backups
- ✅ Secure
- ✅ Scalable
- ✅ Cost-effective
- ✅ Monitoring via CloudWatch

---

##  Supported Database Engines in RDS

- MySQL
- PostgreSQL
- MariaDB
- Oracle
- Microsoft SQL Server
- Amazon Aurora (AWS-made, MySQL/PostgreSQL compatible)

---

##  Simple RDS Workflow

1. Open **AWS Console**
2. Go to **RDS** service
3. Click **Create Database**
4. Select **Engine** (e.g., MySQL)
5. Set DB name, master username and password
6. Choose instance size and storage
7. Set networking and security (VPC, security groups)
8. Launch your DB

---

##  RDS Security

- **Username & password**
- **VPC and security groups** to control access
- **Encryption** in-transit (SSL) and at-rest (KMS)

---

## 🧪 Sample SQL Commands

```sql
CREATE DATABASE testdb;
USE testdb;

CREATE TABLE students (
  id INT,
  name VARCHAR(100),
  age INT
);

INSERT INTO students VALUES (1, 'Alice', 20);
SELECT * FROM students;
