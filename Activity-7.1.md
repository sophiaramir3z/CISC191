
# Activity 7.1- Exceptions

## My Flowchart:
<img width="1024" height="768" alt="Brown Pastel Flowchart Diagram Graph Template (2)" src="https://github.com/user-attachments/assets/43ad61d5-f6ac-46ee-93ee-5c803590329e" />

## My challenges in performing the lab:
One challenge I faced was learning how to use exceptions correctly, especially how to throw and catch them in different parts of the program. 
I also had to figure out when to print the “Course Information” line so it only showed for valid input. Getting the output to display two decimal places took some trial and error. 
Handling negative numbers and testing different inputs helped me make sure the program worked as expected.

## My code:
```java
import java.util.Scanner;

public class StepCounter {

    // Method to convert steps to miles
    public static double stepsToMiles(int steps) throws Exception {
        if (steps < 0) {
            throw new Exception("Exception: Negative step count entered.");
        }
        return steps / 2000.0;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int steps = sc.nextInt(); // Read user input

        try {
            double miles = stepsToMiles(steps); // Call method
            System.out.println("Course Information:");
            System.out.printf("%.2f", miles); // Format to two decimals
        } catch (Exception e) {
            System.out.println(e.getMessage()); // Print exception message
        }

        sc.close();
    }
}

```

## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/8bdfe2d8-4405-4b82-aa38-7c4297337f3c
