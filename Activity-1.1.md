# Lab 1: Sorting

## My Flowchart:
![Activity1 1](https://github.com/user-attachments/assets/a05d6c02-9eb0-46e3-b9d8-010cb214639e)

## Why I selected this particular sorting algorithm:
I used Java’s built-in Arrays.sort() with Collections.reverseOrder() because it’s simple, efficient, and reliable. 
It sorts in descending order with less code, making the program easier to read while still meeting all requirements.
## My challenges in performing the lab:
The main challenge was making sure the output matched the required format (comma-separated values). 
I also had to adjust the sorting to work in descending order instead of the default ascending.

## My code:
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Scanner;

public class Main {
    // Method to sort the array in descending order
    public static void sortArray(int[] myArr, int arrSize) {
        // Convert to Integer[] so we can use Collections.reverseOrder
        Integer[] tempArr = new Integer[arrSize];
        for (int i = 0; i < arrSize; i++) {
            tempArr[i] = myArr[i];
        }

        // Sort in descending order
        Arrays.sort(tempArr, Collections.reverseOrder());

        // Copy back into original array
        for (int i = 0; i < arrSize; i++) {
            myArr[i] = tempArr[i];
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Prompt the user for input
        System.out.println("Enter the number of integers followed by the integers themselves:");

        // Read size
        int n = sc.nextInt();
        int[] arr = new int[n];

        // Read elements
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        // Sort array
        sortArray(arr, n);

        // Print sorted array
        for (int i = 0; i < n; i++) {
            if (i > 0) {
                System.out.print(",");
            }
            System.out.print(arr[i]);
        }
    }
}
```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/1a7fe792-b35b-4721-b1f7-e6d96bdea199
