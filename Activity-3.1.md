
# Activity 3.1- Memory management

## My Flowchart:
![Untitled Diagram](https://github.com/user-attachments/assets/eb9e6ec9-f682-4d61-be4d-e2dbc59405cb)

## Mapping: Stack vs. Heap
![IMG_9264](https://github.com/user-attachments/assets/03adb3f4-df6d-4913-b78c-bda769b30958)

## My challenges in performing the lab:
My main challenges in this lab were designing code that clearly shows stack vs. heap usage and object lifetimes, 
ensuring objects actually become eligible for GC, and making garbage collection observable without relying on deprecated methods.

## My code:
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

class Customer {
    private final String id;
    private final String name;

    Customer(String id, String name) {
        this.id = id;
        this.name = name;
    }

    String getId() { return id; }
    String getName() { return name; }
}

class Order {
    private final String orderId;
    private final double amountCents;

    Order(String orderId, double amountCents) {
        this.orderId = orderId;
        this.amountCents = amountCents;
    }

    double getAmountCents() { return amountCents; }
    String getOrderId() { return orderId; }
}

public class MemoryLab {
    public static void main(String[] args) {
        Customer cust = new Customer("C-1001", "Ada Lovelace"); // heap
        List<Order> orders = new ArrayList<>();                 // heap

        for (int i = 1; i <= 3; i++) {
            orders.add(new Order("O-" + i, 1999.0 * i));        // heap
        }

        double discounted = processDailyDiscounts(orders);
        System.out.println("Discounted total: " + discounted);

        orders = null;  // ArrayList + Orders now eligible for GC
        System.gc();    // suggest GC
        byte[] pressure = new byte[20 * 1024 * 1024]; // heap, temp

        // End of main: 'cust' and 'pressure' also become eligible
    }

    private static double processDailyDiscounts(List<Order> todays) {
        double sum = 0.0;                   // stack
        Random rng = new Random();          // heap

        for (Order o : todays) {
            Order tmpOrder = new Order(     // heap, short-lived
                o.getOrderId() + "-disc",
                o.getAmountCents() * (0.95 + 0.01 * rng.nextInt(3))
            );
            sum += tmpOrder.getAmountCents();
            // tmpOrder reference dies after each iteration
        }
        return sum;
    }
}

```
## Explanation Video:
