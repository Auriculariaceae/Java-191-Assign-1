#This is my first assignment
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        //Task 1.1 – Variable Declaration
        int a = 5;
        int b = 10;
        double d1 = 15.55;
        char c1 = 'k';
        boolean b1 = true;
        System.out.println(a);
        System.out.println(b);
        System.out.println(d1);
        System.out.println(c1);
        System.out.println(b1);
        //Task 1.2 – Arithmetic Operations
        System.out.println(a + b);
        System.out.println(a - b);
        System.out.println(a * b);
        double q1 = (double) a / b;
        System.out.println(q1);
        System.out.println(a % b);
        //Task 2.1 – Basic Input
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter your name:");
        String name = sc.nextLine();
        System.out.println("Enter your age:");
        int age = sc.nextInt();
        int i = age + 1;
        System.out.println("Hello " + name + ", you will be " + i + " next year.");
        //Task 2.2 – Comparing Numbers
        System.out.println("Please enter two different numbers");
        int first = sc.nextInt();
        int second = sc.nextInt();
        if (first > second)
            System.out.println(first);
        else
            System.out.println(second);
        //Task 3.1 – if / else
        System.out.println("Enter an integer");
        int c = sc.nextInt();
        if (c > 0) {
            System.out.println("Positive");
        }
        if (c < 0) {
            System.out.println("Negative");
        } else if (c == 0)
            System.out.println("Zero");
        //Task 3.2 - switch
        System.out.println("Enter a number between 1 and 7");
        int day = sc.nextInt();
        switch (day) {
            case 1:
                System.out.println("Sunday");
                break;
            case 2:
                System.out.println("Monday");
                break;
            case 3:
                System.out.println("Tuesday");
                break;
            case 4:
                System.out.println("Wednesday");
                break;
            case 5:
                System.out.println("Thursday");
                break;
            case 6:
                System.out.println("Friday");
                break;
            case 7:
                System.out.println("Saturday");

        }
        //Task 4.1 – for Loop
        for (int a3 = 1; a3 < 21; a3++) {
            System.out.println(a3);
        }
        //Task 4.3 - Nested Loops
        int rows = 5;  //rows are the horizontal element

        for (int g = 1; g <= rows; g++) {  //outer loop
            for (int g1 = 1; g1 <= g; g1++) {
                System.out.print("* ");
            }
            System.out.println(); //moves to a next line to make the triangle
        }

        //Task 5.1 - Array Input
        sc.nextLine();
        int[] numbers = new int[5];
        System.out.println("Enter 5 numbers");
        for (int k = 0; k <= 4; k++) {
            numbers[k] = sc.nextInt();

        }
        for (int k = 0; k <= 4; k++) {
            System.out.println(numbers[k]);
        }
        double sum = 0;
        for (int k = 0; k <= 4; k++) {
            sum += numbers[k];
        }
        double average = sum / numbers.length;
        System.out.println("Array Sum:" + sum);
        System.out.println("Array Average:" + average);

        //Task 5.2 - Min & Max
        int highest = 0;
        for (int k = 0; k <= 4; k++) {
            if (numbers[k] > highest) {
                highest = numbers[k];
            }
        }
        int lowest = numbers[0];
        for (int k = 0; k <= 4; k++) {
            if (numbers[k] < lowest) {
                lowest = numbers[k];
            }

        }

        System.out.println("Array high:" + highest);
        System.out.println("Array low:" + lowest);

        //Part 6: Mini Program
        System.out.println("How many students are in the class?");
        int count = sc.nextInt();
        int[] grades = new int[count];

        for (int s1 = 0; s1 < grades.length; s1++) {
            System.out.println("Enter exam scores");
            grades[s1] = sc.nextInt();
        }
        double sum1 = 0;
        for (int s1 = 0; s1 < grades.length; s1++) {
            sum1 += grades[s1];
        }
        double average1 = sum1 / grades.length;

        int highestExam = 0;
        for (int s1 = 0; s1 < grades.length; s1++) {
            if (grades[s1] > highestExam) {
                highestExam = grades[s1];
            }
        int studentsPassed = 0;
        for ( s1 = 0; s1 < grades.length; s1++) {
            if (grades[s1]>=60){
                studentsPassed++;
            }
        }
            System.out.println("Exam High: " +highestExam);
            System.out.println("Exam average: " +average1);
            System.out.println("Students passed: " +studentsPassed);
        }
    }
}
```


'''  
