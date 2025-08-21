# 📌 Project Setup Details

**Project Title:** Connecting Amazon EC2 to Amazon RDS

---

## 🔹 Step 1: Create an RDS Database

1. Go to the **AWS Management Console → RDS**.
2. Click **Create Database**.
3. Choose **Standard Create**.
4. Select **MySQL** (or PostgreSQL / Aurora if required).
5. Choose **Free Tier** (for testing).
6. Enter details:

   * DB Name → `storage`
   * Master Username → `admin`
   * Master Password → `Sharan$009` (example)
7. Choose **DB Instance Size** → `db.t3.micro` (free tier).
8. Storage → General Purpose SSD (20GB).
9. VPC → Default VPC.
10. Public Access → **Yes** (for testing, can disable in production).
11. Create the database.

✅ Once created, copy the **RDS Endpoint** (e.g., `database.ctekuaec69qd.ap-south-1.rds.amazonaws.com`).

---

## 🔹 Step 2: Configure RDS Security Group

1. Go to **EC2 → Security Groups**.
2. Find the **RDS Security Group**.
3. Add an **Inbound Rule**:

   * Type → MySQL/Aurora
   * Port → `3306`
   * Source → Security Group of EC2 instance (best practice).

---

## 🔹 Step 3: Launch an EC2 Instance

1. Go to **EC2 Console → Launch Instance**.
2. Choose **Amazon Linux 2 / Ubuntu**.
3. Instance Type → `t2.micro` (free tier).
4. Key Pair → Create or choose existing key.
5. Security Group → Allow:

   * SSH (Port 22) → My IP
   * MySQL (Port 3306) → RDS Security Group (for testing, you may allow all TCP).
6. Launch the instance.

---

## 🔹 Step 4: Install Java Software on EC2

## Do Your Queries here....

