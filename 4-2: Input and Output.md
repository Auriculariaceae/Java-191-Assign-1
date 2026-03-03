```java
//replace all _photo.jpg with _info.txt  in the ParkPhotos.txt
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;

public class PhotoList {
    public static void main(String[] args) throws IOException {
        FileInputStream fileByteStream = null; // File input stream
        Scanner inFS = null;                   // Scanner object
        String fileName;                           // Data value from file

        // Try to open file
        System.out.println("Opening file ParkPhotos.txt.");
        fileByteStream = new FileInputStream("ParkPhotos.txt");
        inFS = new Scanner(fileByteStream);

        List<String> lines = Files.readAllLines(Paths.get("ParkPhotos.txt")); //Paths.get(" ") turns a string into a file system path. It's like a String Wrapper for a file path.
        //Files.readAllLines();  Opens the file, reads every line, stores each line as a separate string in a new ArrayList<String>, and returns List<String>
        //List over ArrayList because we don't need ArrayList exclusive method. And .readAllLines is for List type inputs.
        System.out.println("Reading and modifying photo names.");

        for (int i = 0; i < lines.size(); i++) {  //changes all the file names to _info.txt
            try {                                //"_photo.jpg"   _info.txt
                fileName = lines.get(i);  //lines is array name
                fileName = fileName.replace("_photo.jpg", "_info.txt"); // Replaces ending
                lines.set(i, fileName);  // Update the line in the list
                Files.createFile(Paths.get(fileName));  //creates the file from the updated name
                System.out.println("Name of Photo: " + fileName); //checker to make sure _photos.jpg can be read  if not changed then _photo.jpg will still pop up
            } catch (java.nio.file.FileAlreadyExistsException ignored) {
                //nothing happens as file already exists aka ignored
            }
            for (i = 0; i < lines.size(); i++) {
                System.out.println(lines.get(i));  //prints updated file names OR whatever is in the ParkPhotos.txt
            }
            Files.write(Paths.get("ParkPhotos.txt"), lines); //takes modified list of photo names and save it back into .txt file replacing old contents


            System.out.println("Files created!");
            System.out.println("Closing file");
            inFS.close();  //closing is good etiquette
            fileByteStream.close(); // close() may throw IOException if fails
        }
    }
}
```



### Some challenges I faced in this lab is understanding what Paths. (essentially creates an object reference to a system stored file) is, setting up the for loops correctly,
### and I had to lookup why I should use a List<String> instead of ArrayList<String>  --> List<String> is the input for Files.readAllLines and an ArrayList isn't as flexible as a list
