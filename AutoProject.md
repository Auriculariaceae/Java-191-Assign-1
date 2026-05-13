``` java
import java.sql.*;
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;
import java.util.regex.*;

public class AutoProject {
    public static void main(String[] args)
            throws SQLException, ClassNotFoundException, FileNotFoundException {
// Load the JDBC driver
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        // Establish a connection
        // Assuming the database name is 'auto', user is 'testuser'
        // and password is 'Pa$$word'
        Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/auto", "testuser", "Pa$$word");
        System.out.println("Database connected");

        // Create a statement
        Statement statement = connection.createStatement();


        File auto = new File("auto.txt");
        Scanner autoReader = new Scanner(auto);

        int inserted = 0;
        int skipped = 0;

        while (autoReader.hasNext()) { // && count<1

            String line = autoReader.nextLine().trim();

            if (line.isEmpty()) continue; //ignores empty lines

            String[] autos = line.split(",(?=(?:[^\"]*\"[^\"]*\")*[^\"]*$)");   // Better CSV split that respects quotes.

            String carName = autos[8].replace("\"", "").replace("'", "''");  // remove outer quotes + escape single quotes. allows the use of carName in insertion String

            String insertSQL = "INSERT IGNORE INTO autotable " +
                    "(MPG, Cylinders, Displacement, Horsepower, Weight, Acceleration, `Model Year`, Origin, `Car Name`) " +  //doesn't ignore duplicates :(
                    "VALUES (" + autos[0] + "," + autos[1] + "," + autos[2] + "," + autos[3] + "," +
                    autos[4] + "," + autos[5] + "," + autos[6] + "," + autos[7] +
                    ",'" + carName + "')";

            try {
                int rows = statement.executeUpdate(insertSQL);
                if (rows > 0) {
                    inserted++;
                } else {
                    skipped++;        // This catches duplicates (INSERT IGNORE returns 0)
                }
            } catch (SQLException e) {
                System.out.println("Error inserting: " + e.getMessage());
                skipped++;
            }
            System.out.println("Inserted: " + inserted);
            System.out.println("Skipped (duplicates or bad rows): " + skipped);
        }
        // Close the connection
        connection.close();

    }
}
```
