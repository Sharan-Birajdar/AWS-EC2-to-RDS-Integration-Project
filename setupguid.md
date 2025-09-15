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

Java installation code:-
      sudo yum install java-17-amazon-corretto-devel -y

MySQL installation code:-
      sudo dnf install mariadb105 -y

jdbc driver:-
      wget https://github.com/awslabs/aws-mysql-jdbc/releases/download/1.1.15/aws-mysql-jdbc-1.1.15.jar

## 🔹 Step 6. Connect EC2 to RDS
  -**Use** below code to connect **EC2** to **RDS**

      import java.sql.Connection;
      import java.sql.DriverManager;
      import java.sql.PreparedStatement;
      import java.sql.ResultSet;
      import java.sql.Statement;
      import java.util.Scanner;

    public class UserDatabaseApp {
    // RDS MySQL details
    private static final String JDBC_URL = "jdbc:mysql://database-111.ch8ccwuo4r1w.ap-southeast-2.rds.amazonaws.com:3306/storage";
    private static final String USERNAME = "admin";
    private static final String PASSWORD = "Dara1234";

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Connection conn = null;

        try {
            // Connect to RDS
            conn = DriverManager.getConnection(JDBC_URL, USERNAME, PASSWORD);
            System.out.println("✅ Connected to Database!");

            while (true) {
                System.out.println("\n--- User Menu ---");
                System.out.println("1. Add User");
                System.out.println("2. View Users");
                System.out.println("3. Exit");
                System.out.print("Enter choice: ");
                int choice = sc.nextInt();
                sc.nextLine(); // clear buffer

                if (choice == 1) {
                    // Add User
                    System.out.print("Enter Name: ");
                    String name = sc.nextLine();
                    System.out.print("Enter Address: ");
                    String address = sc.nextLine();
                    System.out.print("Enter Contact: ");
                    String contact = sc.nextLine();

                    String sql = "INSERT INTO users (name, address, contact) VALUES (?, ?, ?)";
                    PreparedStatement pstmt = conn.prepareStatement(sql);
                    pstmt.setString(1, name);
                    pstmt.setString(2, address);
                    pstmt.setString(3, contact);

                    int rows = pstmt.executeUpdate();
                    if (rows > 0) {
                        System.out.println("✅ User added successfully!");
                    }
                    pstmt.close();
                } 
                else if (choice == 2) {
                    // View Users
                    String sql = "SELECT * FROM users";
                    Statement stmt = conn.createStatement();
                    ResultSet rs = stmt.executeQuery(sql);

                    System.out.println("\nID | Name | Address | Contact");
                    System.out.println("-------------------------------------------");
                    while (rs.next()) {
                        int id = rs.getInt("id");
                        String name = rs.getString("name");
                        String address = rs.getString("address");
                        String contact = rs.getString("contact");

                        System.out.println(id + " | " + name + " | " + address + " | " + contact);
                    }
                    rs.close();
                    stmt.close();
                } 
                else if (choice == 3) {
                    System.out.println("👋 Exiting program...");
                    break;
                } 
                else {
                    System.out.println("❌ Invalid choice. Try again.");
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try { if (conn != null) conn.close(); } catch (Exception e) {}
            sc.close();
        }
    }
    }
## 🔹 Step 7. Compile and Run Java Code
