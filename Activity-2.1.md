# Activity 2.1 - Calculate salary using classes


## My Flowchart:
![SalaryCalc](https://github.com/user-attachments/assets/5b7a6f8a-cb41-4b64-a3f6-178ed28280c8)

## My challenges in performing the lab:
My main design challenge was choosing how to make the tax table configurable; 
I compared a setter after construction with an overloaded constructor and supported both while cloning arrays to preserve encapsulation. 
I validated table lengths and ascending thresholds with the last entry as `Integer.MAX_VALUE`, handled bracket edge cases, the sentinel input of minus one, 
and ensured tax uses integer truncation. Implementation friction was mostly IDE related, like matching file names to public class names and running the correct main class.

## TaxTableTools.java code:
```java
public class TaxTableTools {
    private int[] search =   {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
    private double[] value = { 0.0,   0.10,  0.20,   0.30,              0.40 };
    private int nEntries;

    public TaxTableTools() {
        nEntries = search.length;
    }

    // Task A: setter so main can inject tables
    public void setTables(int[] newSearch, double[] newValue) {
        if (newSearch == null || newValue == null) throw new IllegalArgumentException("Tables cannot be null");
        if (newSearch.length != newValue.length) throw new IllegalArgumentException("Tables must match in length");
        this.search = newSearch.clone();
        this.value  = newValue.clone();
        this.nEntries = this.search.length;
    }

    // Task B: overloaded constructor
    public TaxTableTools(int[] searchTable, double[] valueTable) {
        if (searchTable == null || valueTable == null) throw new IllegalArgumentException("Tables cannot be null");
        if (searchTable.length != valueTable.length) throw new IllegalArgumentException("Tables must match in length");
        this.search = searchTable.clone();
        this.value  = valueTable.clone();
        this.nEntries = this.search.length;
    }

    public double getValue(int searchArgument) {
        double result = 0.0;
        int i = 0;
        boolean keepLooking = true;
        while (i < nEntries && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            } else {
                ++i;
            }
        }
        return result;
    }
}

```

## IncomeTaxMainA.java (using classes)
```java
import java.util.Scanner;

public class IncomeTaxMainA {

    public static int getInteger(Scanner input, String prompt) {
        System.out.println(prompt + ": ");
        return input.nextInt();
    }

    public static void main(String[] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);

        int[] salary   = {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
        double[] rates = { 0.0,   0.10,  0.20,   0.30,              0.40 };

        TaxTableTools table = new TaxTableTools();
        table.setTables(salary, rates);   // Task A uses the setter

        int annualSalary = getInteger(scnr, PROMPT_SALARY);
        while (annualSalary >= 0) {
            double taxRate = table.getValue(annualSalary);
            int taxToPay = (int)(annualSalary * taxRate);
            System.out.println("Annual Salary: " + annualSalary +
                    "\tTax rate: " + taxRate +
                    "\tTax to pay: " + taxToPay);
            annualSalary = getInteger(scnr, PROMPT_SALARY);
        }
    }
}

```
## IncomeTaxMainB.java (using constructor overload)
```java
import java.util.Scanner;

public class IncomeTaxMainB {
    public static void main(String[] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);

        // First run: same tables as defaults
        int[]    salaryRange = {   0,  20000, 50000, 100000, Integer.MAX_VALUE };
        double[] taxRates    = { 0.0,   0.10,  0.20,   0.30,              0.40 };

        TaxTableTools table = new TaxTableTools(salaryRange, taxRates); // Task B uses overloaded constructor

        int annualSalary = getInt(scnr, PROMPT_SALARY);
        while (annualSalary >= 0) {
            double taxRate = table.getValue(annualSalary);
            int taxToPay = (int)(annualSalary * taxRate);
            System.out.println("Annual Salary: " + annualSalary +
                    "\tTax rate: " + taxRate +
                    "\tTax to pay: " + taxToPay);
            annualSalary = getInt(scnr, PROMPT_SALARY);
        }
    }

    private static int getInt(Scanner sc, String prompt) {
        System.out.println(prompt + ": ");
        return sc.nextInt();
    }
}

```
## modified tables
```java
int[]    salaryRange = {   0,  30000,  60000,  Integer.MAX_VALUE };
double[] taxRates    = { 0.0,  0.25,   0.35,               0.45 };
```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/544408e8-f663-439e-a497-878e74cfaf57
