# Midterm CISC 191
## Version 1
```java
import java.util.*;

public class InventoryControlV1 {
    private static final Scanner in = new Scanner(System.in);

    private static final List<Painkiller> painkillers = new ArrayList<>();
    private static final List<Bandage> bandages = new ArrayList<>();
    private static final List<EquipmentItem> equipment = new ArrayList<>();

    public static void main(String[] args) {
        System.out.println("Inventory control system - version 1.0");
        while (true) {
            System.out.println("\nChoose a section:");
            System.out.println("1) Painkillers");
            System.out.println("2) Bandages");
            System.out.println("3) Equipment");
            System.out.println("4) Exit");
            String s = in.nextLine().trim();
            if (s.equals("4")) break;

            switch (s) {
                case "1" -> sectionPainkillers();
                case "2" -> sectionBandages();
                case "3" -> sectionEquipment();
                default -> System.out.println("Please choose 1-4.");
            }
        }
        System.out.println("Goodbye.");
    }

    //Base and Derived Classes

    // Parent class
    static class Item {
        protected String nameOfTheItem;
        protected String companyName;

        public Item() { }

        public Item(String nameOfTheItem, String companyName) {
            update(nameOfTheItem, companyName); // overload used
        }

        // Overloaded update: set just the common fields
        public void update(String nameOfTheItem, String companyName) {
            this.nameOfTheItem = nameOfTheItem;
            this.companyName = companyName;
        }

        // Interactive updates
        public void update(Scanner in) {
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();
        }

        // Will be overridden
        public void display() {
            System.out.println("Item");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
        }
    }

    // Painkillers: name, drug company name, expiry date, age group
    static class Painkiller extends Item {
        private String expiryDate; // keep as free text for simplicity
        private String ageGroup;

        public Painkiller() { }

        // Overloaded constructor
        public Painkiller(String name, String company, String expiryDate, String ageGroup) {
            super(name, company);
            this.expiryDate = expiryDate;
            this.ageGroup = ageGroup;
        }

        // Override & Overload update
        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Painkillers]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("drug company name: ");
            companyName = in.nextLine().trim();

            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();

            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();
        }

        // Overridden display
        @Override
        public void display() {
            System.out.println("Painkillers");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- drug company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
        }
    }

    // Bandages: name, company name, expiry date, age group, waterproof (Y/N)
    static class Bandage extends Item {
        private String expiryDate;
        private String ageGroup;
        private boolean waterProof;

        public Bandage() { }

        public Bandage(String name, String company, String expiryDate, String ageGroup, boolean waterProof) {
            super(name, company);
            this.expiryDate = expiryDate;
            this.ageGroup = ageGroup;
            this.waterProof = waterProof;
        }

        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Bandages]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();

            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();

            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();

            while (true) {
                System.out.print("water proof (Y/N): ");
                String yn = in.nextLine().trim();
                if (yn.equalsIgnoreCase("Y")) { waterProof = true; break; }
                if (yn.equalsIgnoreCase("N")) { waterProof = false; break; }
                System.out.println("Please enter Y or N.");
            }
        }

        @Override
        public void display() {
            System.out.println("Bandages");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
            System.out.println("- water proof (Y/N): " + (waterProof ? "Y" : "N"));
        }
    }

    // Equipment: name, company name, weight
    static class EquipmentItem extends Item {
        private double itemWeightLbs;

        public EquipmentItem() { }

        public EquipmentItem(String name, String company, double itemWeightLbs) {
            super(name, company);
            this.itemWeightLbs = itemWeightLbs;
        }

        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Equipment]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();

            while (true) {
                System.out.print("item weight (lbs): ");
                String s = in.nextLine().trim();
                try {
                    itemWeightLbs = Double.parseDouble(s);
                    break;
                } catch (NumberFormatException e) {
                    System.out.println("Please enter a number for lbs.");
                }
            }
        }

        @Override
        public void display() {
            System.out.println("Equipment");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- item weight (lbs): " + itemWeightLbs);
        }
    }

    //Section Menus

    private static void sectionPainkillers() {
        while (true) {
            System.out.println("\nPainkillers: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;

            switch (c) {
                case "1" -> {
                    Painkiller p = new Painkiller();
                    p.update(in);                       // interactive update
                    painkillers.add(p);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(painkillers);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionBandages() {
        while (true) {
            System.out.println("\nBandages: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;

            switch (c) {
                case "1" -> {
                    Bandage b = new Bandage();
                    b.update(in);
                    bandages.add(b);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(bandages);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionEquipment() {
        while (true) {
            System.out.println("\nEquipment: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;

            switch (c) {
                case "1" -> {
                    EquipmentItem e = new EquipmentItem();
                    e.update(in);
                    equipment.add(e);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(equipment);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    //display
    private static <T extends Item> void displayList(List<T> list) {
        if (list.isEmpty()) {
            System.out.println("No items yet.");
            return;
        }
        System.out.println("\n--- Display items ---");
        int i = 1;
        for (Item it : list) {
            System.out.println("#" + i++);
            it.display(); // calls the overridden method
        }
    }
}
```

# Version 2 
```java
import java.util.*;

public class InventoryControlV2 {
    private static final Scanner in = new Scanner(System.in);

    private static final List<Painkiller> painkillers = new ArrayList<>();
    private static final List<Bandage> bandages = new ArrayList<>();
    private static final List<EquipmentItem> equipment = new ArrayList<>();

    //Derived exceptions
    static class InvalidYesNoException extends Exception {
        public InvalidYesNoException(String msg) { super(msg); }
    }
    static class InvalidPositiveNumberException extends Exception {
        public InvalidPositiveNumberException(String msg) { super(msg); }
    }

    public static void main(String[] args) {
        System.out.println("Inventory control system - version 2.0");
        while (true) {
            System.out.println("\nChoose a section:");
            System.out.println("1) Painkillers");
            System.out.println("2) Bandages");
            System.out.println("3) Equipment");
            System.out.println("4) Exit");
            String s = in.nextLine().trim();
            if (s.equals("4")) break;

            switch (s) {
                case "1" -> sectionPainkillers();
                case "2" -> sectionBandages();
                case "3" -> sectionEquipment();
                default -> System.out.println("Please choose 1-4.");
            }
        }
        System.out.println("Goodbye.");
    }

    // Parent class
    static class Item {
        protected String nameOfTheItem;
        protected String companyName;

        public Item() { }
        public Item(String nameOfTheItem, String companyName) {
            update(nameOfTheItem, companyName);
        }

        // overload
        public void update(String nameOfTheItem, String companyName) {
            this.nameOfTheItem = nameOfTheItem;
            this.companyName = companyName;
        }

        // declare a checked exception so subclasses can throw their own
        public void update(Scanner in) throws Exception {
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();
        }

        public void display() {
            System.out.println("Item");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
        }
    }

    // Painkillers: name, drug company name, expiry date, age group
    static class Painkiller extends Item {
        private String expiryDate;
        private String ageGroup;

        public Painkiller() { }
        public Painkiller(String n, String c, String e, String a) {
            super(n, c); this.expiryDate = e; this.ageGroup = a;
        }

        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Painkillers]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("drug company name: ");
            companyName = in.nextLine().trim();

            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();

            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();
        }

        @Override
        public void display() {
            System.out.println("Painkillers");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- drug company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
        }
    }

    // Bandages: name, company name, expiry date, age group, waterproof (Y/N)
    static class Bandage extends Item {
        private String expiryDate;
        private String ageGroup;
        private boolean waterProof;

        public Bandage() { }
        public Bandage(String n, String c, String e, String a, boolean w) {
            super(n, c); this.expiryDate = e; this.ageGroup = a; this.waterProof = w;
        }

        @Override
        public void update(Scanner in) throws InvalidYesNoException {
            System.out.println("\n[Update Bandages]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();

            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();

            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();

            System.out.print("water proof (Y/N): ");
            String yn = in.nextLine().trim();
            if (yn.equalsIgnoreCase("Y")) waterProof = true;
            else if (yn.equalsIgnoreCase("N")) waterProof = false;
            else throw new InvalidYesNoException("water proof must be Y or N.");
        }

        @Override
        public void display() {
            System.out.println("Bandages");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
            System.out.println("- water proof (Y/N): " + (waterProof ? "Y" : "N"));
        }
    }

    // Equipment: name, company name, item weight
    static class EquipmentItem extends Item {
        private double itemWeightLbs;

        public EquipmentItem() { }
        public EquipmentItem(String n, String c, double w) {
            super(n, c); this.itemWeightLbs = w;
        }

        @Override
        public void update(Scanner in) throws InvalidPositiveNumberException {
            System.out.println("\n[Update Equipment]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();

            System.out.print("company name: ");
            companyName = in.nextLine().trim();

            System.out.print("item weight (lbs): ");
            String s = in.nextLine().trim();
            try {
                double v = Double.parseDouble(s);
                if (v <= 0) throw new InvalidPositiveNumberException("item weight (lbs) must be a positive number.");
                itemWeightLbs = v;
            } catch (NumberFormatException nfe) {
                throw new InvalidPositiveNumberException("item weight (lbs) must be a number.");
            }
        }

        @Override
        public void display() {
            System.out.println("Equipment");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- item weight (lbs): " + itemWeightLbs);
        }
    }

    // Section menus
    private static void sectionPainkillers() {
        while (true) {
            System.out.println("\nPainkillers: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    Painkiller p = new Painkiller();
                    p.update(in);
                    painkillers.add(p);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(painkillers);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionBandages() {
        while (true) {
            System.out.println("\nBandages: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    Bandage b = new Bandage();
                    try {
                        b.update(in);
                        bandages.add(b);
                        System.out.println("Saved.");
                    } catch (InvalidYesNoException e) {
                        System.out.println("Input error: " + e.getMessage());
                    }
                }
                case "2" -> displayList(bandages);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionEquipment() {
        while (true) {
            System.out.println("\nEquipment: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    EquipmentItem e = new EquipmentItem();
                    try {
                        e.update(in);
                        equipment.add(e);
                        System.out.println("Saved.");
                    } catch (InvalidPositiveNumberException ex) {
                        System.out.println("Input error: " + ex.getMessage());
                    }
                }
                case "2" -> displayList(equipment);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static <T extends Item> void displayList(List<T> list) {
        if (list.isEmpty()) {
            System.out.println("No items yet.");
            return;
        }
        System.out.println("\n--- Display items ---");
        int i = 1;
        for (Item it : list) {
            System.out.println("#" + i++);
            it.display();
        }
    }
}
```

## Version 3
```java
import java.util.*;

public class InventoryControlV3 {
    private static final Scanner in = new Scanner(System.in);

    private static final List<Painkiller> painkillers = new ArrayList<>();
    private static final List<Bandage> bandages = new ArrayList<>();
    private static final List<EquipmentItem> equipment = new ArrayList<>();

    // Customized derived exception
    static class InvalidYesNoException extends Exception {
        public InvalidYesNoException(String msg) { super(msg); }
    }

    public static void main(String[] args) {
        System.out.println("Inventory control system - version 3.0");
        while (true) {
            System.out.println("\nChoose a section:");
            System.out.println("1) Painkillers");
            System.out.println("2) Bandages");
            System.out.println("3) Equipment");
            System.out.println("4) Exit");
            String s = in.nextLine().trim();
            if (s.equals("4")) break;

            switch (s) {
                case "1" -> sectionPainkillers();
                case "2" -> sectionBandages();
                case "3" -> sectionEquipment();
                default -> System.out.println("Please choose 1-4.");
            }
        }
        System.out.println("Goodbye.");
    }

    //Parent class
    static class Item {
        protected String nameOfTheItem;
        protected String companyName;

        public Item() { }
        public Item(String nameOfTheItem, String companyName) {
            update(nameOfTheItem, companyName); // overload
        }
        public void update(String nameOfTheItem, String companyName) {
            this.nameOfTheItem = nameOfTheItem;
            this.companyName = companyName;
        }
        // Declare a checked exception so subclasses may throw their own
        public void update(Scanner in) throws Exception {
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();
            System.out.print("company name: ");
            companyName = in.nextLine().trim();
        }
        public void display() {
            System.out.println("Item");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
        }
    }

    //Derived classes
    // Painkillers: name, drug company name, expiry date, age group
    static class Painkiller extends Item {
        private String expiryDate;
        private String ageGroup;

        public Painkiller() { }
        public Painkiller(String n, String c, String e, String a) {
            super(n, c); this.expiryDate = e; this.ageGroup = a;
        }

        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Painkillers]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();
            System.out.print("drug company name: ");
            companyName = in.nextLine().trim();
            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();
            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();
        }

        @Override
        public void display() {
            System.out.println("Painkillers");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- drug company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
        }
    }

    // Bandages: name, company name, expiry date, age group, water proof (Y/N)
    static class Bandage extends Item {
        private String expiryDate;
        private String ageGroup;
        private boolean waterProof;

        public Bandage() { }
        public Bandage(String n, String c, String e, String a, boolean w) {
            super(n, c); this.expiryDate = e; this.ageGroup = a; this.waterProof = w;
        }

        @Override
        public void update(Scanner in) throws InvalidYesNoException {
            System.out.println("\n[Update Bandages]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();
            System.out.print("company name: ");
            companyName = in.nextLine().trim();
            System.out.print("expiry date: ");
            expiryDate = in.nextLine().trim();
            System.out.print("age group: ");
            ageGroup = in.nextLine().trim();

            System.out.print("water proof (Y/N): ");
            String yn = in.nextLine().trim();
            if (yn.equalsIgnoreCase("Y")) waterProof = true;
            else if (yn.equalsIgnoreCase("N")) waterProof = false;
            else throw new InvalidYesNoException("water proof must be Y or N.");
        }

        @Override
        public void display() {
            System.out.println("Bandages");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- expiry date: " + expiryDate);
            System.out.println("- age group: " + ageGroup);
            System.out.println("- water proof (Y/N): " + (waterProof ? "Y" : "N"));
        }
    }

    // Equipment: name, company name, item weight (lbs)
    static class EquipmentItem extends Item {
        private double itemWeightLbs;

        public EquipmentItem() { }
        public EquipmentItem(String n, String c, double w) {
            super(n, c); this.itemWeightLbs = w;
        }

        @Override
        public void update(Scanner in) {
            System.out.println("\n[Update Equipment]");
            System.out.print("Name of the item: ");
            nameOfTheItem = in.nextLine().trim();
            System.out.print("company name: ");
            companyName = in.nextLine().trim();
            // keep weight simple for v3.0 (no custom exception here)
            while (true) {
                System.out.print("item weight (lbs): ");
                try {
                    itemWeightLbs = Double.parseDouble(in.nextLine().trim());
                    break;
                } catch (NumberFormatException e) {
                    System.out.println("Please enter a number.");
                }
            }
        }

        @Override
        public void display() {
            System.out.println("Equipment");
            System.out.println("- Name of the item: " + nameOfTheItem);
            System.out.println("- company name: " + companyName);
            System.out.println("- item weight (lbs): " + itemWeightLbs);
        }
    }

    //Menus (catch one invalid input)
    private static void sectionPainkillers() {
        while (true) {
            System.out.println("\nPainkillers: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    Painkiller p = new Painkiller();
                    p.update(in);
                    painkillers.add(p);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(painkillers);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionBandages() {
        while (true) {
            System.out.println("\nBandages: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    Bandage b = new Bandage();
                    try {
                        b.update(in);                    // may throw InvalidYesNoException
                        bandages.add(b);
                        System.out.println("Saved.");
                    } catch (InvalidYesNoException e) {   // catch one invalid input
                        System.out.println("Input error: " + e.getMessage());
                    }
                }
                case "2" -> displayList(bandages);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static void sectionEquipment() {
        while (true) {
            System.out.println("\nEquipment: 1) add/update  2) display  3) back");
            String c = in.nextLine().trim();
            if (c.equals("3")) return;
            switch (c) {
                case "1" -> {
                    EquipmentItem e = new EquipmentItem();
                    e.update(in);
                    equipment.add(e);
                    System.out.println("Saved.");
                }
                case "2" -> displayList(equipment);
                default -> System.out.println("Choose 1-3.");
            }
        }
    }

    private static <T extends Item> void displayList(List<T> list) {
        if (list.isEmpty()) {
            System.out.println("No items yet.");
            return;
        }
        System.out.println("\n--- Display items ---");
        int i = 1;
        for (Item it : list) {
            System.out.println("#" + i++);
            it.display();
        }
    }
}
```
