---
title: Java Database Connectivity (JDBC) 
date: 2023-11-07 10:28:05
toc: true  
categories:  
- java  

---

# Java Database Connectivity (JDBC)

Java Database Connectivity (JDBC) is an API for connecting and executing database queries in Java. It provides a standard interface for Java applications to interact with various database management systems (DBMS).

### Detailed Description of JDBC Working Mechanism and Key Components:

1. **JDBC Driver**: Implementations provided by database vendors to connect to different types of databases. For example, Oracle and MySQL have their own JDBC drivers.
2. **Connecting to Database**: Use the `DriverManager` class to establish a connection to the database by providing the database URL, username, and password.
3. **Executing SQL Statements**: Use `Statement`, `PreparedStatement`, and `CallableStatement` objects to execute SQL statements.
   - `Statement` executes static SQL statements.
   - `PreparedStatement` executes parameterized SQL statements.
   - `CallableStatement` executes stored procedures.
4. **Handling Result Sets**: After executing a query (SELECT statement), a `ResultSet` object is returned, containing the query results. You can traverse this result set to retrieve data.
5. **Closing Connections**: After database operations are complete, close the `ResultSet`, `Statement`, and database connection to release resources.
   - `close()`: Immediately release the database and JDBC resources held by this `Connection` object rather than waiting for them to be automatically released.
6. **Transaction Management**: JDBC supports transactions, which can be controlled by the database connection to start, commit, and roll back transactions.
   - `setAutoCommit(boolean autoCommit)`: Set whether the connection's transactions are automatically committed.
   - `commit()`: Commit the current transaction.
   - `rollback()`: Roll back the current transaction.
7. **Exception Handling**: JDBC operations can throw `SQLException`. Proper handling of these exceptions is crucial for building robust database applications.

### A Basic JDBC Usage Example

In this example, we connect to a MySQL database, execute a query, and print the data from the result set. Note that in a real application, you should handle exceptions properly and ensure resources are released correctly.

```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        try {
            // Load the driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Establish the connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "username", "password");

            // Create the statement
            Statement stmt = con.createStatement();

            // Execute the query
            ResultSet rs = stmt.executeQuery("select * from users");

            // Process the result set
            while (rs.next()) {
                System.out.println(rs.getInt(1) + "  " + rs.getString(2));
            }

            // Close the connections
            rs.close();
            stmt.close();
            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```