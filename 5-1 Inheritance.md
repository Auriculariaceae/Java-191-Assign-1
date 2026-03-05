```java
// ===== Code from file Person.java =====
public class Person {
    private int ageYears;     //originally private, but I wanted to use it in student child class methods, so must be protected
    private String lastName;

    public void setName(String userName) {
        lastName  = userName;
    }
    public String getName(){
        return lastName;
    }
    public void setAge(int numYears) {
        ageYears = numYears;
    }
    public int getAge(){
        return ageYears;
    }
    // Other parts omitted

    public void printAll() {
        System.out.print("Name: " + getName());
        System.out.print(", Age: "  + getAge());
    }
}
// ===== end =====
// ===== Code from file Student.java =====
public class Student extends Person {
    private int idNum;

    public void setID(int studentId) {
        idNum = studentId;
    }

    public int getID() {
        return idNum;
    }
@Override
public void printAll() {
    System.out.println("Name: "+getName() +", Age: "+getAge()+ ", ID "+getID());
}
}
// ===== end =====
// ===== Code from file StudentDerivationFromPerson.java =====
public class StudentDerivationFromPerson {
    public static void main(String[] args) {
        Student courseStudent = new Student();
        courseStudent.setName("Smith");
        courseStudent.setAge(20);
        courseStudent.setID(9999);
        courseStudent.printAll();
    }
}
```
For this specific assignment I didn't run into any challenges asides from needing to use a getter method in my printAll() method because the properties are private in the main class.



