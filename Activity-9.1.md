# Activity 9.1 - Collections

## My Flowchart:
![Collections](https://github.com/user-attachments/assets/9bdd13f8-466a-41fb-aef0-e90870fecb5e)

## My challenges in performing the lab:
One challenge was deciding how to handle spaces and punctuation. I learned that using regular expressions like replaceAll("[^a-zA-Z]", "") helps clean the input efficiently. 
Another difficulty was understanding how a deque works - specifically the difference between removeFirst() and removeLast(). 
After debugging, I realized a deque allows checking from both ends, making it perfect for palindrome checking. Once I figured out the flow, the logic became clear and straightforward.

## My code:
```java
import java.util.*;

public class PalindromeChecker {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String text = input.nextLine();

        // Clean the input (remove punctuation and spaces, lowercase)
        text = text.replaceAll("[^a-zA-Z]", "").toLowerCase();

        // Create a Deque of characters
        Deque<Character> deque = new ArrayDeque<>();

        // Add all characters to the deque
        for (char c : text.toCharArray()) {
            deque.add(c);
        }

        // Check palindrome by comparing front and back
        boolean isPalindrome = true;
        while (deque.size() > 1) {
            if (deque.removeFirst() != deque.removeLast()) {
                isPalindrome = false;
                break;
            }
        }

        // Display result
        if (isPalindrome) {
            System.out.println("Yes, " + text + " is a palindrome.");
        } else {
            System.out.println("No, \"" + text + "\" is not a palindrome.");
        }
    }
}
```

## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/6123509a-bdd0-4ea0-a53b-e2e6dddd53d5
