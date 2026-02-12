
```java

public static void main(String [] args) {
    //Task 1.1 --- Manual Boxing
    System.out.println("Task 1.1 --- Manual Boxing");

    int x = 50;
    Integer x1 = Integer.valueOf(x);
    System.out.println("int: " + x);
    System.out.println("Integer: " + x1);

    //Task 1.2 --- Auto Boxing and Unboxing
    System.out.println("Task 1.2 --- Auto Boxing and Unboxing");

    Integer y = 10;
    System.out.println("Integer: " + y);
    Integer y1 = 20;
    int num = y1;
    System.out.println("int from wrapper: " + num);

    System.out.println("Reflection Questions\n 1.) Primitive data types store raw data. They aren't objects and can't use methods.\n     Wrapper references are objects, are able to use methods, and works with generics.\n 2.) Autoboxing occurs during compiling.");

    //Task 2.1 --- Convert String to Integer
    System.out.println("Task 2.1 --- Convert String to Integer");
    String r = "123";
    Integer r1 = Integer.parseInt(r);
    System.out.println(r1 + 10);

    //Task 2.2 --- Print Limits
    System.out.println("Task 2.2 --- Print Limits");
    System.out.println("Integer minimum value:" + Integer.MIN_VALUE + "\nInteger maximum value: " + Integer.MAX_VALUE);
    System.out.println("Reflection Question\nThey allow us to use the absolute max and min of what the data type allows for sorting or other calculations.");

    //Task 3 --- Wrapper Classes with Arraylist
    System.out.println("Task 3 --- Wrapper Classes with Arraylist");
    ArrayList<Integer> list = new ArrayList<>();
    int sum = 0;
    int loopLimit = 6;
    for (int i = 1; i <= loopLimit; i++) {
        int additionValue = (i) * 25;
        list.add(additionValue);
        System.out.println("Value " + i +" :"+additionValue);
        sum = sum + additionValue;
    }

    System.out.println("Sum: "+sum);
    System.out.println("Question\nArrayList<int> doesn't work because int is a primitive data type and <> requires an object.");

    //Task 4 --- Character Wrapper
    System.out.println("Task 4 --- Character Wrapper");
    char J = '9';
    System.out.println("True/False: Is the character uppercase?");
    System.out.println(Character.isUpperCase(J));
    System.out.println("True/False: Is the character a digit?");
    System.out.println(Character.isDigit(J));
    System.out.println("True/False: Is the character a letter?");
    System.out.println(Character.isLetter(J));
}

```
