# Activity: GUI input and ActionListeners

## My Flowchart:
![Gui1](https://github.com/user-attachments/assets/beb01436-afc0-410c-9a7c-5ee74ef6e286)

## My challenges in performing the lab:
The main challenge was connecting the GUI components with the logic using an ActionListener. 
Initially, I had trouble retrieving input values from the JTextFields because I didn’t parse them correctly as doubles. 
Another challenge was ensuring the layout looked organized and easy to use. 
I resolved these by experimenting with GridLayout and using Double.parseDouble() within a try-catch block to handle invalid input gracefully.

## My code:
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class SalaryCalculator extends JFrame implements ActionListener {
    private JTextField wageField, hoursField;
    private JLabel resultLabel;

    public SalaryCalculator() {
        setTitle("Yearly Salary Calculator");
        setSize(350, 200);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new GridLayout(4, 2, 10, 10));

        // Labels
        add(new JLabel("Hourly Wage ($):"));
        wageField = new JTextField();
        add(wageField);

        add(new JLabel("Hours per Week:"));
        hoursField = new JTextField();
        add(hoursField);

        JButton calcButton = new JButton("Calculate");
        calcButton.addActionListener(this);
        add(calcButton);

        resultLabel = new JLabel("Yearly Salary: ");
        add(resultLabel);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        try {
            double wage = Double.parseDouble(wageField.getText());
            double hours = Double.parseDouble(hoursField.getText());
            double yearlySalary = wage * hours * 52;
            resultLabel.setText(String.format("Yearly Salary: $%.2f", yearlySalary));
        } catch (NumberFormatException ex) {
            resultLabel.setText("Please enter valid numbers.");
        }
    }

    public static void main(String[] args) {
        new SalaryCalculator();
    }
}

```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/884d983e-7fd1-435e-a026-eb4b515601dc
