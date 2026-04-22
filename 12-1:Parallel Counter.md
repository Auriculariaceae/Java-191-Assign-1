```java
class Counter {
    int value = 0;

    synchronized void increment() {
        value++;
    }
}

public class Main {
    public static void main(String[] args) throws Exception {

        Counter counter = new Counter();  //counter class

        // Runnable task
        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();   // critical section   uses the class to use methods
            }
            for (int i = 1; i <= 5; i++) {
                System.out.println(Thread.currentThread().getName() + " : " + i);
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {}
            }
        };


        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);
        //Start of Task 3
        Thread t3 = new Thread(task);
        Thread t4 = new Thread(task);
        Thread t5 = new Thread(task);


        t1.start();
        t2.start();
        t3.start();
        t4.start();
        t5.start();

        t1.join();
        t2.join();
        t3.join();
        t4.join();
        t5.join();

        System.out.println("Final Counter: " + counter.value);
    }

}

//Task 1: Ran 5 times and all 5 came out as 2000
//Task 2: Same thing as Task 1. All 5 runs came out to 2000
//Task 3: Increase to 5 threads and each increments 1000 times
```
### Refelection
## Why does the incorrect result occur? 
# I don't really know the answer to this, but I do know that when I run the program multiple times the output for the sleep tasks changes every time I run it.
## What is a race condition?
# A race condition happens when mutliple threads attempt to modify the same data.
## Why does synchronized fix the issue?
# Synchronization forces exclusion for the data being accessed/modified. Two threads can't modify the same data at the same time
## Does more threads always mean faster execution?
# NO
