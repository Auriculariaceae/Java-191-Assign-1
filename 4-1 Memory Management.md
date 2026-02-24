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

int i = 11;
Double Q = 1700.00;
}
```

# Stack

|Memory Address|Content|Variable|Explanation|
|-|-|-|-|
|0x100|0xA|memory|reference to Student in heap|
|0x200|11|i|
|0x300|0xC|Q|reference to Wrapped Double Q|

# Heap
|Memory Address|Content|Variable|Explanation|
|-|-|-|-|
|0x2000|Student Object||Actual student object|
|0x2010|0xB|this.name|primitive data types in Student class|
|0x2020|200|this.age|  
|0x2030|3.76|this.gpa|
|0x3000|Wowza||Student object Name|
|0x4000|1700.00|Q|Wrapped Double Q|

