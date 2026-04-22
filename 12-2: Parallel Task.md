```java

import java.util.concurrent.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws Exception {
        long start = System.currentTimeMillis();
        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<Integer>> tasks = List.of(
                () -> {
                    Thread.sleep(3000);
                    return 10;
                },
                () -> {
                    Thread.sleep(1000);
                    return 20;
                },
                () -> {
                    Thread.sleep(2000);
                    return 30;
                }
        );
        //Part B:
        int fastestResult = executor.invokeAny(tasks);
        System.out.println("Fastest Result: " + fastestResult);

        //Part C:
        List<Future<Integer>> results = executor.invokeAll(tasks);

        int sum = 0;
         for (Future<Integer> f : results) {  //for (int i = 0; i < results.size(); i++) { //basic for loop
                                                //Future<Integer> f = results.get(i);
            sum += f.get();
        }

        System.out.println("Sum of all results: " + sum);

         //Part D:
        CompletionService<Integer> service =
                new ExecutorCompletionService<>(executor);

        for (Callable<Integer> task : tasks) {
            service.submit(task);
        }

        System.out.println("Results in completion order:");

        for (int i = 0; i < tasks.size(); i++) {
            Future<Integer> result = service.take();
            System.out.println(result.get());
        }
        //Part E


// run tasks
        long end = System.currentTimeMillis();
        System.out.println("Time: " + (double) (end - start)/1000 +"seconds");
    }



}

```

# Reflection Questions
## Why does invokeAny return early?
 It invokes all tasks at the same time and then returns the value that finishes first and stops the other tasks.
## When should you use invokeAll?
 When you need all values of the tasks. invokeAll will run all tasks and return all values.
## How does CompletionService improve performance?
 CompletionService processes tasks at the same time and returns the completion values by order of completion not order of code.
## Does more threads always mean faster execution?
 NOOOO




