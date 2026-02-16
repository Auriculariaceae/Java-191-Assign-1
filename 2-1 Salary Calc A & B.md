### Part A TaxTableTools 

```java
public class TaxTableTools {

    /** This class searches the 'search' table with a search argument and
     returns the corresponding value in the 'value' table. Variable
     'nEntries' has the number of entries in each table.
     */
    private int [] search =   {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
    private double [] value = { 0.0,   0.10,  0.20,   0.30,              0.40 };
    private int nEntries;

    // ***********************************************************************

    // Default constructor
    public TaxTableTools () {
        nEntries  = search.length;  // Set the length of the search table
    }

    // ***********************************************************************

    void setTables(){
        int [] newSearch= { 0, 40000, 80000,300000, Integer.MAX_VALUE};
        search = newSearch;
        double [] newValue = { 0, 0.40, 0.30, 0.10, 0.05 };
        value = newValue;
    }

    // FIXME: Write a void setter method that sets new values for the private
    //        search and value tables. Name the method: setTables
    //        The method receives as parameters tables from which to load the
    //        search and value tables.

    // ***********************************************************************

    // Method to get a value from one table based on a range in the other table

    public double getValue(int searchArgument) {
        double result;
        boolean keepLooking;
        int i;

        result = 0.0;
        keepLooking = true;
        i = 0;

        while ((i < nEntries) && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            }
            else {
                ++i;
            }
        }

        return result;
    }
} 

```
### Part A Income Tax Main

```java 
import java.util.Scanner;

public class IncomeTaxMain {

    // Method to prompt for and input an integer
    public static int getInteger(Scanner input, String prompt) {
        int inputValue;

        System.out.println(prompt + ": ");
        inputValue = input.nextInt();

        return inputValue;
    } //

    // ***********************************************************************

    public static void main(String [] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);
        int annualSalary;
        double taxRate;
        int taxToPay;
        int i;

        int []    salary   = {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
        double [] taxTable = { 0.0,   0.10,  0.20,   0.30,              0.40 };

        // Access the related class
        TaxTableTools table = new TaxTableTools();
        table.setTables();
        // FIXME: Call a setter method in the TaxTableClass that supplies new
        //        tables for the class to work with. The method should be called
        //        with: table.setTables(salary, taxTable);

        // Get the first annual salary to process
        annualSalary = getInteger(scnr, PROMPT_SALARY);

        while (annualSalary >= 0) {
            taxRate = table.getValue(annualSalary);
            taxToPay= (int)(annualSalary * taxRate);     // Truncate tax to an integer amount
            System.out.println("Annual Salary: " + annualSalary +
                    "\tTax rate: " + taxRate +
                    "\tTax to pay: " + taxToPay);

            // Get the next annual salary
            annualSalary = getInteger(scnr, PROMPT_SALARY);
        }
    }
}
```
### Part B TaxTableTools
```java

import java.util.Scanner;

public class TaxTableTools {

    /** This class searches the 'search' table with a search argument and
     returns the corresponding value in the 'value' table. Variable
     'nEntries' has the number of entries in each table.
     */
    private int [] search =   {   0, 20000, 50000, 100000,  Integer.MAX_VALUE };
    private double [] value = { 0.0,  0.10,  0.20,   0.30,               0.40 };
    private int nEntries;

    // ***********************************************************************

    // Default constructor

    public TaxTableTools () {
        nEntries  = search.length;  // Set the length of the search table


    }

    // ***********************************************************************

    // Overloaded constructor
    public TaxTableTools (int[] search, double[] value) {
        nEntries  = search.length;   // Set the length of the search table
        this.search = search;
        this.value = value;
    }
    // FIXME: Add an overloaded constructor to load the search and value tables.
    // FIXME: Be sure to set the nEntries value, too.

    // ***********************************************************************

    // Method to prompt for and input an integer

    public int getInteger(Scanner input, String prompt) {
        int inputValue = 0;

        System.out.println(prompt + ": ");
        inputValue = input.nextInt();

        return inputValue;
    }

    // ***********************************************************************

    // Method to get a value from one table based on a range in the other table

    public double getValue(int searchArgument) {
        double result;
        boolean keepLooking;
        int i;

        result = 0.0;
        keepLooking = true;
        i = 0;

        while ((i < nEntries) && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            }
            else {
                ++i;
            }
        }

        return result;
    }
} 

```
### Part B IncomeTaxMain

```java

import java.util.Scanner;

public class IncomeTaxMain {
    public static void main(String [] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);
        int annualSalary;
        double taxRate;
        int taxToPay;
        int i;

        // Tables to use in the exercise are the same as in the TaxTableTools class
         //int [] salaryRange = {   0,  20000, 50000, 100000,  Integer.MAX_VALUE };
       // double [] taxRates = { 0.0,   0.10,  0.20,   0.30,               0.40 };

        // 2(a) Modify the salary and tax tables in the main method to use
        // different salary ranges and tax rates.
        int []    salaryRange  = {   0,  45000,  85000,  Integer.MAX_VALUE };
        double [] taxRates     = { 0.0,  0.20,   0.24,               0.08 };

        // Access the related class
        // TaxTableTools table = new TaxTableTools();

        // 2(b)Use the just-created overloaded constructor to initialize
        // the salary and tax tables.
        TaxTableTools table = new TaxTableTools(salaryRange, taxRates);

        // Get the first annual salary to process
        annualSalary = table.getInteger(scnr, PROMPT_SALARY);

        while (annualSalary >= 0) {
            taxRate = table.getValue(annualSalary);
            taxToPay= (int)(annualSalary * taxRate);     // Truncate tax to an integer amount
            System.out.println("Annual Salary: " + annualSalary +
                    "\tTax rate: " + taxRate +
                    "\tTax to pay: " + taxToPay);

            // Get the next annual salary
            annualSalary = table.getInteger(scnr, PROMPT_SALARY);
        }
    }
} 

```

# Challenges:<br/> 
The main challenge with this activity was understanding what an overloaded constructor really was. <br/>
I also had to learn how to use "this.". Because we are keeping search as search then --> this.search = search; is needed <br/>
otherwise we have search = search; which doesn't work. However, after googling the other usages of "this." I am confused as to the other reasons. 
