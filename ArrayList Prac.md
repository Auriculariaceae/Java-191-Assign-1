```java


import java.util.ArrayList;

public static int linearSearch(ArrayList<Integer> list, int target) {
    for (int i = 0; i < list.size(); i++){
        if (list.get(i)==target){
            System.out.println("Index:" +i);
            return i;
        }
    }
    System.out.println("Index not found");
    return -1;
}

void main() {
Scanner sc = new Scanner(System.in);
//Part 1 -- Creating and Using an ArrayList
ArrayList<Integer> scores = new ArrayList<>();
    scores.add(85);
    scores.add(92);
    scores.add(78);
    scores.add(90);
    scores.add(88);
    System.out.println("Scores:" + scores);
    System.out.println("Size:" + scores.size());
// Concept check. int[] arr = new int[5]; creates a basic array of 5 blocks. ArrayList makes an arraylist that can be whatever size
//ArrayList autoboxes int double boolean into an object. It does not store primitive types directly
//Part 2 -- Traversing the ArrayList
System.out.println("For Loop");
for (int i = 0; i<scores.size();i ++){
    System.out.println("Score "+(i+1)+": " + scores.get(i));
}
System.out.println("For-Each Loop");
int i = 1;
    for (Integer score : scores) {
        System.out.println("Score " +i+": " +score);
        i++;
    }
System.out.println(".forEach() Loop");
scores.forEach(score -> System.out.println("Scores: " +score));
//The regular for loop has access to the index
//Part 3 -- Modifying Elements
System.out.println("Part 3 -- Modifying Elements");
for (i = 0; i<scores.size(); i++){
    if (scores.get(i)==78){
        scores.set(i, 80);
        break;
    }
}
    for (i = 0; i<scores.size(); i++){
        if (scores.get(i)==92){
            scores.remove(i);
            break;
        }
    }
    System.out.println("Modified scores:" + scores);

    linearSearch(scores, 90);
    linearSearch(scores, 100);
//Part 5 -- Insertions at Different Positions
    System.out.println("Part 5 -- Insertions at Different Positions");
    scores.add(0,95);
    System.out.println(scores);
    scores.add(2,70);
    System.out.println(scores);
    scores.add(100);
    System.out.println(scores);

//Part 6 -- Mini Project
ArrayList<String> students = new ArrayList<>();

while (true){                              //while (true) is an infinite loop unless an exit is coded and used
    System.out.println("===MENU===");
    System.out.println("1. Add Student");
    System.out.println("2. Remove Student");
    System.out.println("3. Search Student");
    System.out.println("4. Display all Students");
    System.out.println("5. Display Total Count");
    System.out.println("6. Exit");  //needed otherwise infinite
    System.out.println("Please enter a choice (1-6)");

    int selection = sc.nextInt();
    sc.nextLine();

    switch (selection) {
        case 1:
            System.out.println("Add student name: ");
            String newStud = sc.nextLine();
            students.add(newStud);
        break;
        case 2:
            System.out.println("Remove student name(Case-Sensitive):  ");
            String remStud = sc.nextLine();
            students.remove(remStud);
        break;
        case 3:
            System.out.println("Search for a student: ");
            String searchStud = sc.nextLine();
            for (String foundStudent : students){
                if(foundStudent.equals(searchStud)){
                System.out.println("Found student: "+foundStudent);
                break;
            }
            else{                                        //this else makes it so that it can only find anything in index[0] but the loop will continue
                System.out.println(searchStud +" not found.");

                }
            }
                break;                    //tricky break without it here case 3 always runs 4 as well >:|
        case 4:
            System.out.println("Display all current students");
            for (i = 0; i<students.size();i++){
                System.out.println(students.get(i));
            }break;
        case 5:
            System.out.println("Total students: "+students.size());
            break;
        case 6:
            System.out.println("Exiting program.");
            sc.close();
            break;

        default:
        // nada

    }

       //I mean it does close
}
}


```

