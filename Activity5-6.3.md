# Activity 5-6.3- Overriding methods

## My Flowchart:
<img width="371" height="461" alt="6 3 drawio" src="https://github.com/user-attachments/assets/d4b3ff63-df82-4c36-9582-1b0c0b331509" />

## My challenges in performing the lab:
One challenge was making sure the overridden printInfo() in Encyclopedia included all the details from the base Book class without duplicating code. 
To solve this, I reused the base class’ method and then added the extra fields. Another challenge was carefully handling input order so the correct values were assigned to the right object. 
This reinforced the importance of planning the structure before writing the code.

## My code:
```java
import java.util.Scanner;

class Book {
    private String title;
    private String author;
    private String publisher;
    private String publicationDate;

    public void setTitle(String t) {
        title = t;
    }

    public void setAuthor(String a) {
        author = a;
    }

    public void setPublisher(String p) {
        publisher = p;
    }

    public void setPublicationDate(String d) {
        publicationDate = d;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public String getPublisher() {
        return publisher;
    }

    public String getPublicationDate() {
        return publicationDate;
    }

    public void printInfo() {
        System.out.println("Book Information: ");
        System.out.println("   Book Title: " + title);
        System.out.println("   Author: " + author);
        System.out.println("   Publisher: " + publisher);
        System.out.println("   Publication Date: " + publicationDate);
    }
}

class Encyclopedia extends Book {
    private String edition;
    private int numPages;

    public void setEdition(String e) {
        edition = e;
    }

    public void setNumPages(int n) {
        numPages = n;
    }

    public String getEdition() {
        return edition;
    }

    public int getNumPages() {
        return numPages;
    }

    @Override
    public void printInfo() {
        super.printInfo();
        System.out.println("   Edition: " + edition);
        System.out.println("   Number of Pages: " + numPages);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scnr = new Scanner(System.in);

        Book book1 = new Book();
        book1.setTitle(scnr.nextLine());
        book1.setAuthor(scnr.nextLine());
        book1.setPublisher(scnr.nextLine());
        book1.setPublicationDate(scnr.nextLine());

        Encyclopedia book2 = new Encyclopedia();
        book2.setTitle(scnr.nextLine());
        book2.setAuthor(scnr.nextLine());
        book2.setPublisher(scnr.nextLine());
        book2.setPublicationDate(scnr.nextLine());
        book2.setEdition(scnr.nextLine());
        book2.setNumPages(Integer.parseInt(scnr.nextLine()));

        book1.printInfo();
        book2.printInfo();
    }
}
```

## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/f4dff543-568c-4880-98d5-5035f2bf3dc1
