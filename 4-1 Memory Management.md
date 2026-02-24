```java
//explain where everything is stored (Draw the tables for stack and heap)

public class Student {
    String name;
    int age;
    double gpa;

public void setName(String name){
    this.name = name;
}
public void setAge(int age){
    this.age = age;
}
public void setGpa(double gpa){
    this.gpa=gpa;
}
public void displayInfo(){
    System.out.println("Name: "+name + " Age: "+age + " GPA: "+gpa);
}
}
void main() {
    Student memory = new Student();
    memory.setName("Wowza");
    memory.setAge(200);
    memory.setGpa(3.76);
    memory.displayInfo();
}
```

# Stack
