```java
// ===== Code from file Person.java =====
public class Person {
    protected int ageYears;     //originally private, but I wanted to use it in student child class methods, so must be protected
    protected String lastName;

    public void setName(String userName) {
        lastName  = userName;
    }

    public void setAge(int numYears) {
        ageYears = numYears;
    }

    // Other parts omitted

    public void printAll() {
        System.out.print("Name: " + lastName);
        System.out.print(", Age: "  + ageYears);
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
    System.out.println("Name: "+lastName +", Age: "+ageYears+ ", ID "+idNum);
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
For this specific assignment I didn't run into any challenges. When using the Overriden method printAll() in 
the child class Student, I had to make the initial properties of the Person class into protected instead of private, so that
my child class's method can utilize them. 



