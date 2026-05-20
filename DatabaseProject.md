# First code is for uploading from java to a database
```java
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
                    "(MPG, Cylinders, Displacement, Horsepower, Weight, Acceleration, `Model Year`, Origin, `Car Name`, `Unique ID`) " +  //doesn't ignore duplicates :(
                    "VALUES (" + autos[0] + "," + autos[1] + "," + autos[2] + "," + autos[3] + "," +
                    autos[4] + "," + autos[5] + "," + autos[6] + "," + autos[7] +
                    ",'" + carName + "'," + autos[9] + ")";

            try {
                int rows = statement.executeUpdate(insertSQL);
                if (rows > 0) {
                    inserted++;
                } else {
                    skipped++;        // This catches duplicates (INSERT IGNORE returns 0) Doesn't work though :(
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
# Second code is the gui elements
```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;
import java.sql.*;
import java.io.FileNotFoundException;
import java.net.URL;
import javax.imageio.ImageIO;
import java.awt.Image;

public class AutoSearchButtonFrame extends JFrame implements ActionListener {
    private JLabel userInLabel;     // Label for user Input
    private JLabel autoInfoLabel;      // Label for Auto Info
    private JLabel warningLabel;      //Warning Label
    private JTextField inputField;  // Input for car lookup
    private JTextArea autoArea; // Displays auto info
    private JButton searchButton;   // Triggers search
    private JButton resetButton;  // Resets the page to default
    private JButton allButton;

    //All of this before constructor is for a background image
    // Custom panel that draws the background image
    private class BackgroundPanel extends JPanel { //this is a custom panel
        private Image backgroundImage;  //this variable actually holds the image

        public BackgroundPanel() {  //constructor for my class
            try { //try is needed as we are connecting to the internet
                // Replace this URL with your actual image link
                URL imageUrl = new URL("https://d3i6fh83elv35t.cloudfront.net/static/2023/03/2017-01-16T120000Z_2044270320_RC11FA7C4E70_RTRMADP_3_CHINA-AUTOS-SALES-1024x620.jpg");
                backgroundImage = ImageIO.read(imageUrl);
            } catch (Exception e) {
                System.out.println("Failed to load background image: " + e.getMessage());
                // Fallback color if image fails to load
                setBackground(new Color(255, 255, 255)); //set to default white so user has no idea if image fails to load
            }
            setOpaque(false); // Important so components on top are visible
        }

        @Override //this is where the image is drawn. we are ovverriding default painting behabior of JPanel
        protected void paintComponent(Graphics g) {
            super.paintComponent(g); /*super calls the method in the parent class of JPanel. the .paintComponent(g) actually draws the image.
            Basically says "First, do everything regular JPanel does when it paints
            It also clears out leftover pixels, flickering, and artifacts(anomalies)*/
            if (backgroundImage != null) { //this if is so that if it does fail and is null it won't try to "draw" the image
                // Scales image to fill the entire frame
                g.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this);  //0,0 is top left. the get's stretch the image to fill the window, 'this' is a required parameter
            }
        }
    }


    /* Constructor creates GUI components and adds GUI components
       using a GridBagLayout. */
    AutoSearchButtonFrame() {
        // Set background image panel
        BackgroundPanel backgroundPanel = new BackgroundPanel();
        backgroundPanel.setLayout(new GridBagLayout());  //maintains original layout
        setContentPane(backgroundPanel);                 // This makes it the background
        // Used to specify GUI component layout
        GridBagConstraints positionConst = null;

        // Set frame's title
        setTitle("Auto Search Program");

        // Set labels and all formatting
        userInLabel = new JLabel("User Input:");
        userInLabel.setOpaque(true);
        userInLabel.setBackground(new Color(0, 0, 0, 180));     // semi-transparent black
        userInLabel.setBorder(BorderFactory.createCompoundBorder( // all of this is so that user can differentiate the labels from the background
                BorderFactory.createLineBorder(Color.WHITE, 2),   // white outline
                BorderFactory.createEmptyBorder(5, 8, 5, 8)));   // padding inside
        userInLabel.setForeground(Color.GREEN);

        warningLabel = new JLabel("Name of car / Partial names accepted");
        warningLabel.setOpaque(true);
        warningLabel.setBackground(new Color(0, 0, 0, 180));
        warningLabel.setBorder(BorderFactory.createCompoundBorder( // all of this is so that user can differentiate the labels from the background
                BorderFactory.createLineBorder(Color.RED, 2),
                BorderFactory.createEmptyBorder(5, 8, 5, 8)));
        warningLabel.setForeground(Color.RED);

        autoInfoLabel = new JLabel("Auto Info:");
        autoInfoLabel.setOpaque(true);
        autoInfoLabel.setBackground(new Color(0, 0, 0, 180));
        autoInfoLabel.setBorder(BorderFactory.createCompoundBorder( // all of this is so that user can differentiate the labels from the background
                BorderFactory.createLineBorder(Color.WHITE, 2),
                BorderFactory.createEmptyBorder(5, 8, 5, 8)));
        autoInfoLabel.setForeground(Color.GREEN);

        inputField = new JTextField(30);
        inputField.setEditable(true);
        inputField.setText("");

        autoArea = new JTextArea(15, 40);
        autoArea.setEditable(false);
        autoArea.setBackground(Color.WHITE); //this is put in so it isn't grey and the reset works better
        JScrollPane scrollPane = new JScrollPane(autoArea);
        scrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
        scrollPane.setHorizontalScrollBarPolicy(JScrollPane.HORIZONTAL_SCROLLBAR_AS_NEEDED);

        // Create a "Calculate" button
        searchButton = new JButton("Search");

        // Create a "Reset" button
        resetButton = new JButton("Reset");
        resetButton.addActionListener(e -> {
            inputField.setText("");
            autoArea.setText("");
            inputField.setBackground(Color.WHITE);
            autoArea.setBackground(Color.WHITE);
        });
        allButton = new JButton("All Vehicles");
        allButton.addActionListener(e->{
            try {
                String all = callerMethod(""); //empty string here means show everything
                autoArea.setText(all);
            } catch (SQLException | ClassNotFoundException ex) {
                throw new RuntimeException(ex);
            }
        });
        // Use "this" class to handle button presses
        searchButton.addActionListener(this);  //using "this" calls the actionPerformed(ActionEvent event) method

        // Use a GridBagLayout

        positionConst = new GridBagConstraints();

        // Specify component's grid location
        positionConst.gridx = 0;
        positionConst.gridy = 1;

        // 10 pixels of padding around component
        positionConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(userInLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 0;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(warningLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 1);
        add(inputField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(autoInfoLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(scrollPane, positionConst);

        positionConst.gridx = 2;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 1, 10, 10);
        add(searchButton, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 3;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(resetButton, positionConst);

        positionConst.gridx = 2;
        positionConst.gridy = 3;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(allButton, positionConst);
    }

    /* Method is automatically called when an event occurs
    This method is fully for the search button. It essentially looks up what user asks
     and prints it in the text area*/
//this method is parameterized so we can pass the userInput from button press to this method. searchTerm=userInput
    public String callerMethod(String searchTerm) throws SQLException, ClassNotFoundException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        System.out.println("Driver loaded");

        StringBuilder result = new StringBuilder(); //String builder is used because so many .appends will be used. Without it more and more string objects are created. Bad memory usage.

        // Establish a connection
        // Assuming the database name is 'auto', user is 'testuser'
        // and password is 'Pa$$word'
        try (Connection connection = DriverManager.getConnection
                ("jdbc:mysql://localhost/auto", "testuser", "Pa$$word");
             PreparedStatement statement = connection.prepareStatement(
                     "SELECT * FROM autotable WHERE `Car Name` LIKE ? ORDER BY `Model Year`")) {

            System.out.println("Database connected");
/* this line is what allows us to use ? in previous code. the ? is a placeholder
 for whatever user types into inputfield. The 1 is a reference to the 1 ? that's after LIKE
 more ? would mean more searchable terms */
            statement.setString(1, "%" + searchTerm + "%");
            ResultSet resultSet = statement.executeQuery(); //the SQL method that looks for what we want

            // Iterate through the result and print the details of the car
            while (resultSet.next()) {  //.append is used because the data is going to a JTextArea
                result.append(resultSet.getString(1)).append("\t") //this line is where we put our String pieces into our stringbuilder
                        .append(resultSet.getString(2)).append("\t")
                        .append(resultSet.getString(3)).append("\t")
                        .append(resultSet.getString(4)).append("\t")
                        .append(resultSet.getString(5)).append("\t")
                        .append(resultSet.getString(6)).append("\t")
                        .append(resultSet.getString(7)).append("\t")
                        .append(resultSet.getString(8)).append("\t")
                        .append(resultSet.getString(9)).append("\t")
                        .append("\n");
            }
        } catch (SQLException e) {
            result.append("Database Error: ").append(e.getMessage());
            throw e;
        }

        return result.toString(); //all the data is built and this actually gives us the data as a string that's displayed
    }


    @Override
    public void actionPerformed(ActionEvent event) {
        String userInput = inputField.getText().trim(); //grabs user input and assigns it to userInput
        try {
            String results = callerMethod(userInput); //puts userInput into method. Method reads userInput as searchTerm. searchTerm = userInput.
            autoArea.setText(results);
        } catch (SQLException | ClassNotFoundException e) { //multiple exceptions needed for previous code. IDE did it for me
            throw new RuntimeException(e);
        }
    }

    public static void main(String[] args) throws SQLException, ClassNotFoundException, FileNotFoundException {
        {
            // Creates SalaryLabelFrame and its components
            AutoSearchButtonFrame myFrame = new AutoSearchButtonFrame();

            myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            myFrame.pack(); //auto sizes the frame to fit components
            myFrame.setVisible(true);
        }
    }
}
```
