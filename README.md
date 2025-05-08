# SmartCart
Final Project for Object-Oriented Programming

## ✅ Requirements

- **NetBeans IDE** with Java EE support
- **Java JDK** 8 or newer
- **Apache Tomcat** server
- **MySQL Server** installed and running
- **MySQL JDBC Driver** (Connector/J)

## 🛠 MySQL Setup

1. Start your MySQL server.
2. Create the database:

   ```sql
   CREATE DATABASE smartcart;
   ```
3. Create a user and grant access:
   
   ```sql
   CREATE USER 'webuser'@'localhost' IDENTIFIED BY 'yourpassword';
   GRANT ALL PRIVILEGES ON mywebdb.* TO 'webuser'@'localhost';
   FLUSH PRIVILEGES;
   ```
4. Create required tables and insert sample data.
   ```sql
   CREATE TABLE user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(100) NOT NULL
    );
    
    CREATE TABLE budget (
        id INT AUTO_INCREMENT PRIMARY KEY,
        amount DOUBLE NOT NULL,
        description VARCHAR(255),
        user VARCHAR(50),
        FOREIGN KEY (user) REFERENCES user(username)
            ON DELETE CASCADE
            ON UPDATE CASCADE
    );
    
    CREATE TABLE expense (
        id INT AUTO_INCREMENT PRIMARY KEY,
        amount DOUBLE NOT NULL,
        description VARCHAR(255),
        user VARCHAR(50),
        FOREIGN KEY (user) REFERENCES user(username)
            ON DELETE CASCADE
            ON UPDATE CASCADE
    );
    
    CREATE TABLE cart (
        id INT AUTO_INCREMENT PRIMARY KEY,
        itemName VARCHAR(100) NOT NULL,
        quantity INT NOT NULL,
        price DOUBLE NOT NULL,
        user VARCHAR(50),
        FOREIGN KEY (user) REFERENCES user(username)
            ON DELETE CASCADE
            ON UPDATE CASCADE,
        UNIQUE (itemName, user)
    );
    
    CREATE TABLE inventory (
        id INT AUTO_INCREMENT PRIMARY KEY,
        itemName VARCHAR(100) NOT NULL,
        quantity INT NOT NULL,
        user VARCHAR(50),
        FOREIGN KEY (user) REFERENCES user(username)
            ON DELETE CASCADE
            ON UPDATE CASCADE,
        UNIQUE (itemName, user)
    );
   ```

## ⚙️ Project Configuration

### 1. Add MySQL JDBC Driver

1. Download the [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) (JAR file).
2. In NetBeans:
   - Right-click the `Libraries` folder under your project.
   - Select **Add JAR/Folder**.
   - Browse and add the downloaded `mysql-connector-java-x.x.x.jar` file.

---

### 2. Configure Database Connection in Java

5. Modify these lines based on or DB username and password:
   ```java
   private static final String DB_URL = "jdbc:mysql://localhost:3306/smartcart";
   private static final String DB_USER = "your_username"; // Replace with your DB username
   private static final String DB_PASSWORD = "your_password"; // Replace with your DB password
   ```
   
## 🚀 How to Run the Project in NetBeans

1. **Clone or download the project** into your local machine.

2. **Open NetBeans**, then:
   - Go to **File > Open Project**
   - Select the project folder and open it

3. **Add a Server** (if not configured):
   - Go to **Tools > Servers**
   - Click **Add Server**
   - Choose **Apache Tomcat**, set the install path and click **Finish**

4. **Configure the Project Server**:
   - Right-click the project > **Properties**
   - Under **Run**, set the server to the one you added
   - Ensure context path is correct

5. **Build and Run**:
   - Right-click the project > **Clean and Build**
   - Right-click the project > **Run**

6. **Access the Web App**:
   - Open a browser and go to:  
     `http://localhost:8080/SmartCart-Ant/`

## 🛠 Common Issues

- **Port conflicts**: Make sure no other service is using port 8080.
- **Missing server**: Install and configure the required server in NetBeans.
- **JDK mismatch**: Ensure the project JDK matches the NetBeans JDK settings.

