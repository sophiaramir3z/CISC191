# Lab 2: Words frequency

## My Flowchart:
![wordFrequency](https://github.com/user-attachments/assets/9f7d22d0-5ea6-4af1-a050-abe6c6f66f49)

## How I will perform a frequency analysis of a website if I have to do it:
I would fetch the page HTML, extract visible text, normalize it (lowercase, remove punctuation/stopwords), then compute counts with a hash map and output top words. 
Repeat for multiple pages by following internal links and aggregating counts.
## My challenges in performing the lab:
My main challenge was ensuring case-insensitive counting while preserving the original casing in the printed word.
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/e81ccb9b-e9d9-467b-bf97-509775c937b1
## My code:
```java
import java.util.*;

public class Main {
    // Required method: count case-insensitive matches of currWord in wordsList
    public static int getWordFrequency(String[] wordsList, int listSize, String currWord) {
        int count = 0;
        for (int i = 0; i < listSize; i++) {
            if (wordsList[i].equalsIgnoreCase(currWord)) {
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read a whole line of words (<= 20, space-separated)
        String line = sc.nextLine().trim();
        if (line.isEmpty()) return;

        String[] words = line.split("\\s+");
        int n = Math.min(words.length, 20); // per assignment bound

        // For each word as entered, print its frequency (case-insensitive)
        for (int i = 0; i < n; i++) {
            int freq = getWordFrequency(words, n, words[i]);
            System.out.println(words[i] + " " + freq);
        }
    }
}

```
