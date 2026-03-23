```java
import java.util.LinkedList;
import java.util.Scanner;
import java.util.Deque;
public static void main(String[] args) {

    Scanner sc = new Scanner(System.in);
    System.out.println("Word to be checked");

    boolean continuous = true;
    boolean palindromed = true;
    while(continuous){
        String palin = sc.nextLine().trim().toLowerCase().replace(" ", "");
        Deque<Character> newP = new LinkedList<>();

    for (int i = 0; i < palin.length(); i++) {   //converts string palin into characters  then added to deque
        char c = palin.charAt(i);  //grabs the single character at that position
        newP.addLast(c);  //adds the letters to the Deque in FILO order

    }


   int j = 0; //variable is here so single char doesn't double outputs
    if (newP.size() <= 1) { //only for single char
        System.out.println("This is a palindrome");
        j = 0; //variable is here so single char doesn't double outputs

    }

    while (newP.size() > 1) {
        Character first = newP.removeFirst();
        Character last = newP.removeLast();
        j = 1; //variable is here so single char doesn't double outputs. making it != 0 so output later is only one of them

        if (first != last) {
            System.out.println(palin+" is not a palindrome");
            palindromed = false;
            System.out.println("Try again!");
            break;
        }
    }
     if (palindromed == true && j != 0) {  //can be reduced to just (palindromed) "don't want to"
        System.out.println(palin + " is a palindrome");

    }

    System.out.println("Would you like to continue? 0 for yes and 1 for no");
    boolean binaryChoice = true;//everything with binaryChoice is to handle an exception from not inputting 0 or 1
    while (binaryChoice){
        try{ //try catch is for the iffy choice
            int choice = sc.nextInt();
            sc.nextLine();

                if (choice == 0){
                    System.out.println("Word to be checked.");
                    binaryChoice = false;
                    continue;  //continue from the last while that has scanner and input
    }

                if (choice == 1 ){
                    binaryChoice = false;
                    continuous = false;
                }
                }catch (InputMismatchException e){
                    sc.nextLine();
                    System.out.println("Please enter 0 for yes or 1 for no");


             }
        }
    }
                    sc.close();
}
```

### Challenges
I ran into a few challenges for this lab. The first one I ran into was converting a string input into characters and then adding those characters to the Deque. 
When the word to be checked was only a single character I had to make a work around so that my outputs weren't doubled. I did this by making another condition for my last 
if statement and then changing that condition when a non single character palindrome was entered. Making a working while loop to keep asking for a word resulted in a lot of trial and error. A huge source of annoyance and more trial by error was fully fixing a user messing up an input for choosing to run the program again. 
