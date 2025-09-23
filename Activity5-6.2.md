
# Activity 5-6.2- Derived classes

## My Flowchart:
<img width="400" height="1000" alt="Pink and Yellow Pastel Minimalist Step by Step Infographic" src="https://github.com/user-attachments/assets/8498ec72-278f-493f-b654-8d95f12b2c22" />

## My challenges in performing the lab:
My main challenge was deciding how to split state between the base class and the derived class without duplicating fields. I kept course number and title in Course and layered instructor, 
location, and time in OfferedCourse. I also paid attention to exact output formatting and whitespace so the printout matches the spec. 
It was helpful that the requirements already fixed the field list and method names, which made the design straightforward.

## My code:
Person.java
```java
import java.util.Scanner;

class Course {
    private String courseNumber;
    private String courseTitle;

    public void setCourseNumber(String num) {
        courseNumber = num;
    }

    public void setCourseTitle(String title) {
        courseTitle = title;
    }

    public String getCourseNumber() {
        return courseNumber;
    }

    public String getCourseTitle() {
        return courseTitle;
    }

    public void PrintInfo() {
        System.out.println("Course Information:");
        System.out.println("   Course Number: " + courseNumber);
        System.out.println("   Course Title: " + courseTitle);
    }
}

class OfferedCourse extends Course {
    private String instructorName;
    private String location;
    private String classTime;

    public void setInstructorName(String name) {
        instructorName = name;
    }

    public void setLocation(String loc) {
        location = loc;
    }

    public void setClassTime(String time) {
        classTime = time;
    }

    public String getInstructorName() {
        return instructorName;
    }

    public String getLocation() {
        return location;
    }

    public String getClassTime() {
        return classTime;
    }

    @Override
    public void PrintInfo() {
        // Print base information first
        super.PrintInfo();
        // Then the additional details
        System.out.println("   Instructor Name: " + instructorName);
        System.out.println("   Location: " + location);
        System.out.println("   Class Time: " + classTime);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Expected input order:
        // course1 number, course1 title, course2 number, course2 title,
        // instructor name, location, class time
        String c1Num = sc.nextLine().trim();
        String c1Title = sc.nextLine().trim();
        String c2Num = sc.nextLine().trim();
        String c2Title = sc.nextLine().trim();
        String instr = sc.nextLine().trim();
        String loc = sc.nextLine().trim();
        String time = sc.nextLine().trim();

        Course course1 = new Course();
        course1.setCourseNumber(c1Num);
        course1.setCourseTitle(c1Title);

        OfferedCourse course2 = new OfferedCourse();
        course2.setCourseNumber(c2Num);
        course2.setCourseTitle(c2Title);
        course2.setInstructorName(instr);
        course2.setLocation(loc);
        course2.setClassTime(time);

        // Output
        course1.PrintInfo();
        course2.PrintInfo();

        sc.close();
    }
}

```

## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/2441c405-f521-4e67-95f6-002023e26c8c
