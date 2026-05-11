```java
import java.sql.*;
public class SimpleJdbc {
    public static void main(String[] args)
            throws SQLException, ClassNotFoundException {
        // Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        // Establish a connection
        // Assuming the database name is 'miramar', user is 'testuser'
        // and password is 'Pa$$word'
        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/miramar","testuser","Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();

        // Execute a statement


            String insertSQL = "insert into student (ssn,firstname,mi,lastname,birthDate,street,phone,zipcode,deptId)" +
                    "values ('111222333','Philip','D','Briggs','1951-01-30','NA','NA','NA','1234')";
            String insertZip = "update student set zipcode = 92126 where deptID = '1234'";
            try {
               statement.executeUpdate(insertSQL);

           }catch (SQLException e) {
               System.out.println("wow a duplicate");
           }
            try {
                statement.executeUpdate(insertZip);
            }catch (SQLException d){
                System.out.println("Zipcode update failure");
            }

        //do insertions and shit before doing the query below
        ResultSet resultSet = statement.executeQuery
                ("select * from student;");



        // Iterate through the result and print
        while (resultSet.next())
            System.out.println(resultSet.getString(1) + ": " +
                    resultSet.getString(2) +": "+ resultSet.getString(3) + ": " +
                    resultSet.getString(4) + ": " + resultSet.getString(5)+ ": "
                    + resultSet.getString(6) + ": "+ resultSet.getString(7)+ ": " + resultSet.getString(8)+ ": "
                    + resultSet.getString(9));

        // Close the connection
        connection.close();
    }
}
```
# Challenges
I ran into an issue where where my .executeQuery was closing my set and not allowing for any of my updates or changes to go through. This was fixed by making the 
Query line go after all the updates and insertions. I also had to learn the proper way to insert or update a record in java. I had to create a String
with the SQL code (with proper syntax[worst part]) and then use .executeUpdate() instead of .executeQuery. Query returns and Update() is for inserting, deleting,
or updating the SQL.
