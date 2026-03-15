```java
import java.util.Scanner;

//steps to miles method that has a try catch block for exceptions 2000 steps =(ish) 1 miles
int steps;
double miles = (double) steps;     //(double) is explicit casting for steps into a double it isn't needed, but helps me to remember to use it when needed
boolean running = true;
public void stepsToMiles(){
    Scanner scnr = new Scanner(System.in);

    while(running){    //while loop allows user to keep trying to put in a valid positive integer
        try{
        System.out.println("How many steps did you walk?(Positive integers only)");
        steps = scnr.nextInt();
            if(steps<0){
                throw new Exception("Exception: Negative step count entered."); //this is the exception object ->new 
            }
        miles = (double)steps /2000;               //(double) casting is used here to change steps into a double so the division works into decimals
        System.out.printf("%.2f Steps walked", (double)steps);   //(double) cast is needed everytime we do a double format thing with an integer if we dont convert it into a double variable
        System.out.println(" ");   //without this line then the output bleeds into each other
        System.out.printf("%.2f Miles walked%n", miles);     //%n is better than \n in most cases for this format
        running = false;
    }
        catch (InputMismatchException e1){
            scnr.nextLine();
            System.out.println("Please enter a valid number");
        }
        catch (Exception e) {
            scnr.nextLine();
            System.out.println(e.getMessage());      //built like this so the exception doesn't crash the code
            }
    }

}

void main() {
    stepsToMiles();

    //=====Code below is extra=====
    Scanner sc = new Scanner(System.in);
    System.out.println("Would you like to see the exact amount of miles walked if 2000 steps = 1 mile?");
    System.out.println("Answer with yes/no or y/n");
    String choice = sc.nextLine().trim().toLowerCase();     //.trim() gets rid of all white/blank spaces and .toLowerCase() converts all char into lowercase (easier to parameterize)
    boolean Continue = choice.equals("yes") || choice.equals("y") || choice.equals("yeah") || choice.equals("sure");   //a yes no if else.     | <- pole   two poles || is the same as or
    if (Continue){
        System.out.println("Miles walked: "+miles);
    } else{
        System.out.println("\t\t\t\t\t\t\t\t\tಠ_ಠ");  //\t adds a crazy indent
        sc.close(); //allegedly good practice
    }
}

```
### Challenges
A challenge I ran into was using the print format line correctly. I had to experiment with where things were placed to get the output I wanted. I also had to learn what
explicit casting was and how to use it correctly. As I understand it doing (double) to an integer is the same as converting the int into a double for that line of code only.
