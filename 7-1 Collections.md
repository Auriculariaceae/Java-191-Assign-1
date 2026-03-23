```java
import java.util.LinkedList;
import java.util.Scanner;
import java.util.Deque;




public static void main(String[] args) {

    Scanner sc = new Scanner(System.in);
    System.out.println("Word to be checked");
    String palin = sc.nextLine().trim().toLowerCase();
    Deque<Character> newP = new LinkedList<>();

    for (int i = 0; i < palin.length(); i++) {   //converts string palin into characters  then added to deque
        char c = palin.charAt(i);  //gets character of first letter and every letter after
        newP.addLast(c);  //adds each character to deque individually
    }
    int j = 0; //variable is here so single char doesn't double outputs
    if (newP.size() <= 1) { //only for single char
        System.out.println("This is a palindrome");
        j = 0; //variable is here so single char doesn't double outputs
    }
    boolean palindromed = true;
    while (newP.size() > 1) {
        Character first = newP.removeFirst();
        Character last = newP.removeLast();
        j = 1; //variable is here so single char doesn't double outputs. making it != 0 so output later is only one of them
        if (first != last) {
            System.out.println(palin+" is not a palindrome");
            palindromed = false;
            break;
        }
    }
    if (palindromed == true && j != 0) {  //can be reduced to just (palindromed) "don't want to"
        System.out.println(palin + " is a palindrome");
    }


}

```

### Challenges
I ran into a few challenges for this lab. The first one I ran into was converting a string input into characters and then adding those characters to the Deque. 
When the word to be checked was only a single character I had to make a work around so that my outputs weren't doubled. I did this by making another condition for my last 
if statement and then changing that condition when a non single character palindrome was entered.
