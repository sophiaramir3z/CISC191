# Activity 4.1- Input and output

## My Flowchart:
<img width="1024" height="768" alt="Blue Hue Digital Marketing Graph" src="https://github.com/user-attachments/assets/16df51f0-094f-4cf9-ac7b-c53f8c32e323" />

## My challenges in performing the lab:
My main challenge was deciding what to do if the input file name was wrong or the file was missing. 
Since the prompt does not require error messages, I chose a quiet exit to keep the output clean. 
I also made sure the change only affects the suffix by replacing the exact string _photo.jpg with _info.txt and leaving everything else alone. 
Finally, I tested with an empty file to confirm the program prints nothing.

## My code:
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        if (!sc.hasNextLine()) {
            sc.close();
            return;
        }

        String listFileName = sc.nextLine().trim();
        sc.close();

        try (BufferedReader br = new BufferedReader(new FileReader(listFileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                String name = line.trim();
                if (name.isEmpty()) {
                    continue;
                }
                // Replace the exact suffix segment
                String out = name.replace("_photo.jpg", "_info.txt");
                System.out.println(out);
            }
        } catch (IOException e) {
            // Silently exit as the spec does not require error output
        }
    }
}

```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/4e8771dc-6940-46aa-b8b4-fd25e2d410d8
