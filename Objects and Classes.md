```java

public class Student {
    String name;
    int age;
    double gpa;

//constructor
public Student(String name, int age, double gpa){                         //this.   is in reference to the object it is within referencing something else by the same name
    this.name = name;
    this.age = age;
    this.gpa = gpa;
}
//methods
public String getName(){
    return name;
}
public void setName(String name){
    this.name = name;
}
public int getAge(){
    return age;
    }
public void setAge(int age){
    this.age=age;
}
public double getGpa(){
    return gpa;
}
public void setGpa(double gpa){
    this.gpa = gpa;
}

public void displayInfo(){
System.out.println("Name: "+name + " Age: "+age + " GPA: "+gpa);
}
@Override
public String toString(){                               //reformats so System.out.println(s1);  works
    return "Student name = " + name + ",age = " + age + ",gpa = " + gpa;
}
}
//end of student class
//===========================================
//===========================================
//===========================================
public class BankAccount{
String accountHolder;
double balance;
static int totalAccounts = 0;   //static variable means data is shared

//constructor
public BankAccount(String accountHolder, double balance){
this.accountHolder = accountHolder;
this.balance=balance;
totalAccounts++;   //incrementally adding
}
//methods
public static void getTotalAccounts(){
    System.out.println("Total Accounts: "+totalAccounts);
}
public void deposit(double amount){
balance+=amount;         //same as balance = balance + amount;
}
public void withdraw(double amount){
if(amount<=balance){
   balance-=amount;
} else {
    System.out.println("!!NOT ENOUGH FUNDS!!");
}
}
public void getBalance(){
System.out.println("Current balance: "+balance);
}
@Override
    public String toString(){   //reformat to what it needs to be
        return "Account holder: "+accountHolder + " | Current Balance: $"+balance;
}
}
void main() {
Student s1 = new Student("Joe",24, 3.2);
s1.displayInfo();

s1.setGpa(3.9);
System.out.println(s1);             //crazy formatting issue without overriding toString()
//Part 2
Student s2 = s1;
s2.setName("bob");

s1.displayInfo();
s2.displayInfo();
//Reflection: Both objects changed because they reference the same thing. They are not two separate objects. Just 2 reference to the same object
//Part 3
ArrayList<Student> stud = new ArrayList<>();
    Student d1 = new Student("John",30, 3.0);
    Student d2 = new Student("Joe",31, 3.1);
    Student d3 = new Student("Josh",32, 3.2);
stud.add(0,d1);
stud.add(1,d2);
stud.add(d3); //last in line so no index needed
System.out.println("for Loop");
for (int i = 0; i<stud.size();i++){
    System.out.println(stud.get(i));
}
System.out.println("Enhanced for Loop: ");
for (Student student : stud) {        //enhanced for loop   = less things to write
    System.out.println(student);
}
//part 4 Class with Behavior
BankAccount ac1 = new BankAccount("John", 1000);
ac1.deposit(500);
ac1.withdraw(200);
System.out.println(ac1);

//Part 5 Static vs Instance Members
BankAccount ac2 = new BankAccount("Joe", 3000);
BankAccount ac3 = new BankAccount("Josh", 23300);
BankAccount ac4 = new BankAccount("Charles", 1000112);
ac3.getBalance();
ac2.withdraw(3001);
BankAccount.getTotalAccounts();   //should be 4


//Part 6 Questions
//1. A class is the blueprint from which an object can be made. There is only 1 class named students, but it can make infinite student objects.
//A class also contains variables, methods, and constructors.
//2. Objects are stored in the heap. A longer term storage method.
//3. It creates a new object based off the class and allocates memory on the heap for the new object.
//4. Encapsulation protects internal data, improves security of the system, and makes it easier to change methods.
//5. When an object itself is referenced to be printed the defaulted format is not legible.
    
}

```
