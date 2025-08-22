# AWS-EC2-to-RDS-Integration-Project

![alt text](https://github.com/Sharan-Birajdar/AWS-EC2-to-RDS-Integration-Project/blob/main/doc/Images/architecture.png?raw=true)

## 📌 Project Objective

The goal of this project is to **demonstrate cloud resource integration** by connecting an **EC2 instance** with an **Amazon RDS database**. This setup ensures that data entered through the EC2 instance is stored directly in a managed database without building a full application.

---

## 📌 Project Description

1. A **Relational Database Service (Amazon RDS)** instance was created to host the database (e.g., MySQL).
2. An **EC2 instance** was launched to act as the compute environment.
3. **Java was installed on the EC2 instance**, and a simple program was run to insert records into the RDS database.
4. Networking was configured using **Security Groups** so that the EC2 instance could access the RDS database on port **3306**.
5. Data was successfully inserted into the RDS database directly from the EC2 instance, validating connectivity and integration.

---

## 📌 Architecture Flow

* **User/Admin** → connects to EC2 via SSH.
* **EC2 Instance** → runs commands or a simple Java/JDBC script.
* **Amazon RDS** → stores the entered data.

This project highlights **infrastructure-level integration** between AWS compute and database services.

---

## 📌 Benefits of This Setup

* **Scalable**: EC2 and RDS can scale independently.
* **Secure**: Access controlled using IAM roles and security groups.
* **Managed Database**: No manual DB administration, backups, or patching needed.
* **Reusable Setup**: Can serve as a base for future web apps or backend systems.

