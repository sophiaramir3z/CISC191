
# Activity 10-11.2: GUI (input and ActionListeners)

## My Flowchart:
![GUI2](https://github.com/user-attachments/assets/0ccc38c0-8ded-4f39-a56a-c7bdee9ba34a)

## My challenges in performing the lab:
Some challenges I faced during this lab included parsing the input, formatting the output, and managing the layout. 
The JFormattedTextField does not directly return a double, it returns an Object, so figuring out that I needed to cast it as a Number before converting it to a double took some trial and error. 
Without using String.format, the output values displayed too many decimal places, so I had to format each result to two decimal places for a cleaner look. 
Finally, arranging all the components, the labels, text field, and button, so they were aligned properly using GridLayout required some adjustment and testing to make the interface look balanced and organized.

## My code:
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.text.NumberFormat;

public class DistanceConverter extends JFrame {
    private JFormattedTextField inputField;
    private JLabel kmLabel, mLabel, ftLabel;

    public DistanceConverter() {
        setTitle("Distance Converter");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(5, 1));

        NumberFormat numberFormat = NumberFormat.getNumberInstance();
        inputField = new JFormattedTextField(numberFormat);
        inputField.setValue(0.0);
        add(new JLabel("Enter distance (miles):"));
        add(inputField);

        JButton convertButton = new JButton("Convert");
        add(convertButton);

        kmLabel = new JLabel("Kilometers: ");
        mLabel = new JLabel("Meters: ");
        ftLabel = new JLabel("Feet: ");
        add(kmLabel);
        add(mLabel);
        add(ftLabel);

        convertButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    double miles = ((Number) inputField.getValue()).doubleValue();
                    double km = miles * 1.60934;
                    double m = miles * 1609.34;
                    double ft = miles * 5280;

                    kmLabel.setText("Kilometers: " + String.format("%.2f", km));
                    mLabel.setText("Meters: " + String.format("%.2f", m));
                    ftLabel.setText("Feet: " + String.format("%.2f", ft));
                } catch (Exception ex) {
                    JOptionPane.showMessageDialog(null, "Please enter a valid number.");
                }
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new DistanceConverter().setVisible(true);
            }
        });
    }
}

```
## Explanation Video:
https://sdccd.us-west-2.instructuremedia.com/embed/eb8c4b4b-5a07-4e26-9b9c-5265914fc473
