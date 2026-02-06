#Assignment 1-2
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //Part 1: Data Collection
        System.out.println("How many days of temperature data will be entered.");
        int days = sc.nextInt();
        double[] temperature = new double[days];
        System.out.println("Please enter the temperature for each day.");
        int i;
        for (i = 0; i < temperature.length; i++) {
            temperature[i] = sc.nextInt();
        }
        //Part 2: Mean
        double sum = 0;
        for (i = 0; i < temperature.length; i++) {
            sum += temperature[i];
        }
        double mean = sum / temperature.length;
        System.out.println("Temperature mean: " + mean + "F");
        //Part 3 Sorting the data (Ascending order)

        // double[] sorted = new double[temperature.length];
        for (i = 0; i < temperature.length; i++) {
            for (int j = i + 1; j < temperature.length; j++) {
                if (temperature[i] > temperature[j]) {
                    double temp = temperature[i];
                    temperature[i] = temperature[j];
                    temperature[j] = temp;
                }
            }
        }
        for (i = 0; i < temperature.length; i++) {
            System.out.println(temperature[i] + "F");
        }
        //Part 4: Median  odd-middle value  even-average of both middle values
        if (temperature.length % 2 == 1) {           //odd
            System.out.println(temperature[temperature.length / 2] + "F");
        } else {                                     //even
            double mid1 = temperature[temperature.length / 2 - 1];
            double mid2 = temperature[temperature.length / 2];
            System.out.println((mid1 + mid2) / 2 + "F");
        }
        //Part 5: Range       //highest - lowest to get range
        double highest = temperature[0];
        for (i = 0; i < temperature.length; i++) {
            if (temperature[i] > highest) {
                highest = temperature[i];
            }
        }
        double lowest = temperature[0];
        for (i = 0; i < temperature.length; i++) {
            if (temperature[i] < lowest) {
                lowest = temperature[i];
            }
        }
        System.out.println("Range: " + (highest - lowest) + "F");
        //Part 6: Variance
        double variance=0;
        double temp =0;
        for (i = 0; i < temperature.length; i++) {
            //variance = Σ(x − mean)² / n
            temp += (temperature[i] - mean) * (temperature[i] - mean);
        }
            //temp/n=variance; //not right fxi
            variance = temp/temperature.length;
        //System.out.println(n+"Length");   //checker
        //System.out.println(mean+"F");     //checker
        System.out.println("Variance: "+variance);
        //Part 7: Standard Deviation
        double stanDev = Math.sqrt(variance);
        System.out.println("Standard Deviation: "+stanDev);
        if (stanDev<2){
            System.out.println("Temperatures are very consistent");
        }
        else if (stanDev<5){
            System.out.println("Temperatures show moderate variation");
        }
        else{
            System.out.println("Temperatures vary significantly");
        }
    }
}
```
