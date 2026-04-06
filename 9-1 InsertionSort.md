```java
import java.util.Random;

public class InsertionSort {
    public static void insertionSort(int[] numbers) {
        int i;    //loop control variables   j too
        int j;
        int temp;      // used to moves values around during shifting
        int swap = 0;   //counts how many swaps
        int comparisons=0;  //counts how many comparisons

        for (i = 1; i < numbers.length; ++i) {  //loop that picks which element to insert
            j = i;
            temp = numbers[i];  // saves the current element to insert
            // Insert numbers[i] into sorted part
            // stopping once numbers[i] in correct position

            while (j > 0) {  //continues until beginning of array is reached
                comparisons++;   // Count every comparison

                if (numbers[j - 1] > temp) {   // comparison: is the previous element bigger if yes shifts righ
                    // Shift element
                    numbers[j] = numbers[j - 1];  //shifts larger element to the right
                    swap++;
                    j--;
                } else {
                    break;   // if the left element is not bigger, stop
                }
            }
            numbers[j] = temp;   // place the element in its final position
        }

        System.out.println("Swaps " + swap);
        System.out.println("Comparisons " + comparisons);
    }

    public static void insertionSortD(int[] numbers) {
        int o;
        int k;
        int temp;      // Temporary variable for swap

        for (o = 1; o < numbers.length; ++o) {
            k = o;
            // Insert numbers[i] into sorted part
            // stopping once numbers[i] in correct position
            while (k > 0 && numbers[k] > numbers[k - 1]) {   //what makes this descending is the numbers[k] > numbers[k - 1]  if it was numbers[k] < numbers[k - 1]  it would be ascending

                // Swap numbers[j] and numbers[j - 1]  | This is the part that moves the parts around |
                temp = numbers[k];
                numbers[k] = numbers[k - 1];
                numbers[k - 1] = temp;
                --k;
            }
        }
    }


    public static void main(String[] args) {
        
        int[] numbers = new int[300];
        for (int i=0;i<300;i++){
            numbers[i]=(int)(Math.random() * 1000);
        }

        int i;

        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        insertionSort(numbers);   //by having the public class InsertionSort{ be the first line we can run this line of code. MUST HAVE THIS LINE FIRST

        System.out.print("SORTED Ascending: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();
        insertionSortD(numbers);
        System.out.print("SORTED Descending: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
    }
}
```
### Challenges 
I ran into the challenge of having to break apart my while loop in the selectionSort method into a while loop and an if statement. Without breaking it apart the 
comparisons counter was consistently wrong. I had to look up how to fix it and why each element needed to be moved around. The original code from the lecture is my selectionSortD.
