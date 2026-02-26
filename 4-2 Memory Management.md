# 🧪 Lab: Understanding Memory Management in Java

## 🎯 Learning Objectives

By the end of this lab, students will be able to:

1.  Distinguish between **stack memory** and **heap memory**
2.  Understand how **object references** work in Java
3.  Observe **garbage collection behavior**
4.  Identify potential **memory leaks**
5.  Explain how Java manages memory automatically

------------------------------------------------------------------------

# 📘 Part 1 --- Stack vs Heap

## 🔹 Concept Review

-   **Primitive variables** → stored in stack\
-   **Object references** → stored in stack\
-   **Objects themselves** → stored in heap

------------------------------------------------------------------------

## 📝 Task 1: Trace the Memory

``` java
public class MemoryTest1 {
    public static void main(String[] args) {
        int x = 10;
        String name = "Danish";
        Student s1 = new Student("Ali", 20);

        modify(x, s1);

        System.out.println("x = " + x);
        System.out.println("Student age = " + s1.age);
    }

    static void modify(int x, Student s) {
        x = 50;
        s.age = 99;
    }
}

class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 🔎 Questions

1.  Where is `x` stored?
The variable x is stored in a stack.
3.  Where is `s1` stored?
s1 is a reference to the Student object. References to objects are stored on the stack.
4.  Where is the `Student` object stored?
The actual Student object and its data is stored on the heap.
5.  Why does `x` remain 10 after `modify()`?
X remains 10 because it lives on the Main()'s stack. When modify() is called it gets a copy of x on it's own stack.
Within the modify() method's stack the int x is changed to 50, but nothing is done with it, so it's not seen in the output.
The x variable in the main's stack remains unchanged.
6.  Why does `s1.age` change?
s1.age changes because the main stack stores a reference to the heap object "Student". Both the 
main and modify stacks contain the same reference to the heap object reference. Because it's the same reference
they can both modify and or access the properties of the Student object.
### 🎯 Deliverable

Draw a **memory diagram** showing: - Stack frame of `main` - Stack frame
of `modify` - Heap object(s)
# Main stack
|memory address|content|variable|explanation|
|-|-|-|-|
|0x100|10|x|variable int x = 10|
|0x200|0xA|s1|reference to student object in heap|
|0x300|0xC|name|reference to name property of student object in heap|

# modify stack
|memory address|content|variable|explanation|
|-|-|-|-|
|0x100|50|x|variable int x = 50|
|0x200|0xA|s1|reference to student object in heap|
|0x300|0xB||reference to student object age property in heap|

# Heap
|memory address|content|variable|explanation|
|-|-|-|-|
|0xA|Student object|||
|0xB|20|age|property of student|
|0xC|Danish|name|property of student|
------------------------------------------------------------------------

# 📘 Part 2 --- Object References and Aliasing

## 📝 Task 2: Reference Copying

``` java
public class MemoryTest2 {
    public static void main(String[] args) {
        Student s1 = new Student("Sara", 22);
        Student s2 = s1;

        s2.age = 30;

        System.out.println(s1.age);
    }
}
```

### 🔎 Questions

1.  How many objects are created?
One object is created.
2.  How many references exist?
The variables s1 and s2 and their references exist in the stack. The data of s1 exists in the heap.
s1 is an object and s2 is a variable who references s1's data. 2 references exist. s2>oxa  s1>oxa
3.  Why does modifying `s2` affect `s1`?
Only 1 object and they both have the same references

### 🎯 Deliverable

Explain in 5--7 sentences how reference copying works in Java.

------------------------------------------------------------------------

# 📘 Part 3 --- Garbage Collection

## 🔹 Concept Review

Java automatically reclaims memory for objects that: - Are no longer
referenced - Become unreachable

## 📝 Task 3: Eligible for Garbage Collection

``` java
public class MemoryTest3 {
    public static void main(String[] args) {
        Student s1 = new Student("John", 18);
        Student s2 = new Student("Emma", 19);

        s1 = s2;
    }
}
```

### 🔎 Questions

1.  How many objects are created?
Two
2.  Which object becomes eligible for garbage collection?
s1 because it is no longer referenced
3.  At what line does that happen?
during s1 = s2;
4.  Does Java immediately delete it?
No.
### 🎯 Experiment

Add:

``` java
@Override
protected void finalize() throws Throwable {
    System.out.println("Object is being garbage collected");
}
```

Run multiple times.

Do you always see the message? Why or why not?

------------------------------------------------------------------------

# 📘 Part 4 --- Memory Leak Simulation

## 📝 Task 4: Static Reference Leak

``` java
import java.util.ArrayList;

public class MemoryLeakExample {

    static ArrayList<Student> students = new ArrayList<>();

    public static void main(String[] args) {

        for(int i = 0; i < 100000; i++) {
            students.add(new Student("Student" + i, i));
        }

        System.out.println("Done creating students");
    }
}
```

### 🔎 Questions

1.  Why are these objects NOT garbage collected?
They are all referencable data.
2.  What would you change to fix this?
3.  Modify the code to prevent the leak.
I don't understand 2 and 3 still.
------------------------------------------------------------------------

# 📘 Part 5 --- Forcing Memory Pressure

## 📝 Task 5: OutOfMemoryError

``` java
import java.util.ArrayList;

public class MemoryPressure {
    public static void main(String[] args) {

        ArrayList<int[]> list = new ArrayList<>();

        while(true) {
            list.add(new int[1000000]);
        }
    }
}
```

### 🔎 Questions

1.  What exception occurs?
Out of memory error.
2.  Why does it happen?
Too many arrays were created 
3.  What JVM argument can limit heap size?
-Xmx4g in the configuration editor of intellij
Try running with:

    -Xmx128m

------------------------------------------------------------------------

# 📘 Part 6 --- Reflection / Conceptual Questions

1.  Why doesn't Java allow manual memory deallocation?
Java automatically garbage collects. We code it cleans up.
2.  What is the advantage of garbage collection?
Frees up memory.
3.  What is the trade-off compared to C++?
C++ needs manual garbage collection
4.  What is a "strong reference"?
It is referenced so garbage collection doesn't work for it.

------------------------------------------------------------------------

# 🧠 Advanced Challenge (Optional)

-   Use `Runtime.getRuntime().totalMemory()`\
-   Use `Runtime.getRuntime().freeMemory()`\
-   Track memory before and after object creation\
-   Print memory usage statistics

------------------------------------------------------------------------
