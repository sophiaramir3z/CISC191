# Lab: Document analysis (Honors contract)

## My Flowchart:
<img width="1024" height="768" alt="Modern Pastel Flowchart" src="https://github.com/user-attachments/assets/b7e21fae-c65b-45c4-bcd0-2b99ae7a7011" />

## My challenges in performing the lab:
My biggest challenge was making sure punctuation didn’t interfere with word counting. I also had to test multiple regular expressions to properly clean the text.
Another small issue was remembering to close both the BufferedReader and BufferedWriter to prevent file corruption.

## My code:
```java
import java.io.*;
import java.util.*;

public class DocumentAnalyzer {
    public static void main(String[] args) {
        String inputFile = "song.txt";    // input file name
        String outputFile = "output.txt"; // output file name

        Map<String, Integer> wordCount = new HashMap<>();

        try {
            BufferedReader reader = new BufferedReader(new FileReader(inputFile));
            String line;

            while ((line = reader.readLine()) != null) {
                // remove punctuation, convert to lowercase, and split by spaces
                line = line.replaceAll("[^a-zA-Z ]", "").toLowerCase();
                String[] words = line.split("\\s+");

                for (String word : words) {
                    if (word.length() > 0) {
                        wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
                    }
                }
            }
            reader.close();

            // write results to output.txt
            BufferedWriter writer = new BufferedWriter(new FileWriter(outputFile));
            for (Map.Entry<String, Integer> entry : wordCount.entrySet()) {
                writer.write(entry.getKey() + ": " + entry.getValue());
                writer.newLine();
            }
            writer.close();

            System.out.println("Word count completed. Results saved in " + outputFile);

        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}

```

## Explanation Video:
