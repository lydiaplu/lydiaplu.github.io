---
title: Advanced Usage of JDBC
date: 2023-11-07 20:07:18
toc: true  
categories:  
- java  

---



# Advanced Usage of JDBC

Here are some advanced usage examples of Java JDBC, including connection pool management, transaction control, precompiled SQL statements, etc.

Please note that these examples are for reference only and may need to be adjusted according to your specific database and business logic.

### 1. Connection Pool Management Example (Using Apache Commons DBCP)

```java
import org.apache.commons.dbcp2.BasicDataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class ConnectionPoolExample {
    public static void main(String[] args) throws SQLException {
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setUrl("jdbc:mysql://localhost:3306/mydb");
        dataSource.setUsername("username");
        dataSource.setPassword("password");
        dataSource.setMinIdle(5);
        dataSource.setMaxIdle(10);
        dataSource.setMaxOpenPreparedStatements(100);

        Connection conn = null;
        try {
            conn = dataSource.getConnection();
            // Perform database operations
        } finally {
            if (conn != null) {
                conn.close();
            }
        }
    }
}
```

### 2. Precompiled SQL Statements and Batch Operations

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class PreparedStatementBatchExample {
    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "username", "password")) {
            String sql = "INSERT INTO users (name, email) VALUES (?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
                conn.setAutoCommit(false); // Disable auto-commit

                // Batch insert data
                pstmt.setString(1, "Alice");
                pstmt.setString(2, "alice@example.com");
                pstmt.addBatch();

                pstmt.setString(1, "Bob");
                pstmt.setString(2, "bob@example.com");
                pstmt.addBatch();

                int[] updateCounts = pstmt.executeBatch();
                conn.commit(); // Commit transaction
            } catch (SQLException e) {
                conn.rollback(); // Rollback transaction on exception
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 3. Handling Transactions and Setting Transaction Isolation Level

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class TransactionIsolationExample {
    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "username", "password")) {
            conn.setAutoCommit(false);
            conn.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);

            try (Statement stmt = conn.createStatement()) {
                stmt.executeUpdate("UPDATE accounts SET balance = balance - 100 WHERE user = 'user1'");
                // More database operations...

                conn.commit();
            } catch (SQLException e) {
                conn.rollback();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 4. Using Database Metadata

```java
import java.sql.Connection;
import java.sql.DatabaseMetaData;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;

public class DatabaseMetaDataExample {
    public static void main(String[] args) {
        try (Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "username", "password")) {
            DatabaseMetaData dbMetaData = conn.getMetaData();
            ResultSet rs = dbMetaData.getTables(null, null, "%", null);
            while (rs.next()) {
                System.out.println("Table: " + rs.getString(3));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### 5. Exception Handling and Resource Management

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ExceptionHandlingExample {
    public static void main(String[] args) {
        Connection conn = null;
        try {
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "username", "password");
            // Perform database operations...
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException se) {
                se.printStackTrace();
            }
        }
    }
}
```