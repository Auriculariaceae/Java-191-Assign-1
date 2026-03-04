```java
class Course {
    private String courseNumber;
    private String courseTitle;

    public void setCourseNum(String courseNumber) {
        this.courseNumber = courseNumber;
    }

    public String getCourseNum() {
        return courseNumber;
    }

    public void setCourseTitle(String courseTitle) {
        this.courseTitle = courseTitle;
    }

    public String getCourseTitle() {
        return courseTitle;
    }

    public void printInfo() {
        System.out.println("Course #: " + getCourseNum());
        System.out.println("Course Title: " + getCourseTitle());
    }
}
class OfferedCourse extends Course {
    private String instructorName;
    private String location;
    private String classTime;

    public void setInstructorName(String instructorName){
        this.instructorName = instructorName;
    }
    public String getInstructorName(){
        return instructorName;
    }
    public void setLocation(String location){
        this.location=location;
    }
    public String getLocation(){
        return location;
    }
    public void setClassTime(String classTime){
        this.classTime=classTime;
    }
    public String getClassTime(){
        return classTime;
    }
@Override
public void printInfo() {
    System.out.println("Course #: " + getCourseNum());
    System.out.println("Course Title: "+ getCourseTitle());
    System.out.println("Course Instructor: "+ getInstructorName());
    System.out.println("Course Location: "+ getLocation());
    System.out.println("Course Class Time: "+getClassTime());
}

}

public void main(String[] args) {
Course Comp1 = new Course();
Comp1.setCourseNum("ECE287");
Comp1.setCourseTitle("Digital Systems Design");
Comp1.printInfo();
System.out.println("=================================");
OfferedCourse Comp2 = new OfferedCourse();
Comp2.setCourseNum("ECE387");
Comp2.setCourseTitle("Embedded Systems Design");
Comp2.setInstructorName("Mark Patterson");
Comp2.setLocation("Wilson Hall 231");
Comp2.setClassTime("W/F: 2:00 - 3:30 p.m.");
Comp2.printInfo();
}
```
For this assignment I ran into an issue where the line of code public void main(String[] args) wouldn't work when "void" was "static" I don't know what that means
and why it wouldn't work, but intellij changed it for me. 
