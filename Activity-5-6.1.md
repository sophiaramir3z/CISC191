# Activity 5-6.1- Inheritance 

## My Flowchart:
<img width="1024" height="768" alt="Brown Pastel Flowchart Diagram Graph Template (1)" src="https://github.com/user-attachments/assets/870c7e51-ca49-483c-8b44-e59e44d35441" />

## My challenges in performing the lab:
The main challenge was realizing I had to use the setter methods to assign values before printing, and also remembering that printAll() didn’t include the ID so I had to add it separately. 
I thought it was helpful that the base code was already provided, since it let me focus on understanding inheritance instead of setting up everything from scratch.
## My code:
Person.java
```java
public class Person {
   private int ageYears;
   private String lastName;

   public void setName(String userName) {
      lastName  = userName;
   }

   public void setAge(int numYears) {
      ageYears = numYears;
   }

   public void printAll() {
      System.out.print("Name: " + lastName);
      System.out.print(", Age: "  + ageYears);
   }
}

```
Student.java
```java
public class Student extends Person {
   private int idNum;

   public void setID(int studentId) {
      idNum = studentId;
   }

   public int getID() {
      return idNum;
   }
}
```
StudentDerivationFromPerson.java
```java
public class StudentDerivationFromPerson {
   public static void main(String[] args) {
      Student courseStudent = new Student();

      courseStudent.setName("Smith");
      courseStudent.setAge(20);
      courseStudent.setID(9999);

      courseStudent.printAll();
      System.out.println(", ID: " + courseStudent.getID());
   }
}
```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/a7808f10-6656-4201-a0ed-5a50b493f084
