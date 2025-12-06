🍔 Donny’s Order System

Your friendly console-based fast-food ordering companion

CS 2106 — Object-oriented Programming

Abaya,Lorien Emmanuel A.

Bacorayo, John Bryner R.

Macuha, Czian Gabriel A.

Soriano, Kurt Frederie L.

**Overview**

Customers can examine a menu, place orders, and create receipts with Donny's Order, a Java console-based application. It mimics the ordering procedure in a restaurant through simple text-based communication. The system effectively manages menu items and customer orders using Object-Oriented Programming concepts such as encapsulation, inheritance, polymorphism, and abstraction. It also includes advanced features like a Mood-Based Food Recommendation System, an Allergy-Smart Menu Filter, and an Auto-Budget Ordering System to provide smarter and more personalized ordering. Through automation and organized data handling, this project demonstrates how technology can greatly improve food service operations.


Donny’s Order System is a Java console app that lets you explore a restaurant menu, place orders, and manage your cart all from your terminal!

It’s also a great way to see OOP in action, showcasing encapsulation, inheritance, polymorphism, and abstraction.

With this system, you can:

🍽️ Browse all menu items

🛒 Add meals to your cart

🧾 View a receipt (with an automatic student discount!)

🌶️ Filter items for allergies or preferences

😊 Get recommendations based on your mood

💸 Check what you can order within a budget

🔧 Use admin mode to manage menu items

Project Structure
src/
└── orderapp/
    ├── Main.java          // Program entry point
    ├── MenuItem.java      // Abstract base class
    ├── SingleMeal.java    // Individual meal items
    ├── ComboMeal.java     // Combo meals
    └── OrderSystem.java   // Core functionality


File Highlights:

Main.java – Launches the system and displays the main menu

MenuItem.java – Encapsulated base class for all meals

SingleMeal.java – Standard meal items

ComboMeal.java – Meals that include multiple items

OrderSystem.java – Handles menu, cart, sorting, filtering, and admin tasks

How to Run

Open a terminal in your project folder

javac orderapp/*.java


Start the program

java orderapp.Main

Features
1️⃣ View Menu

See all available meals and combos, with details like calories, price, and category.

2️⃣ Add to Cart

Pick an item by number to add it to your order.

3️⃣ View Cart & Receipt

Check everything in your cart, along with a total bill.

If you’re a student, you automatically get 10% off!

4️⃣ Sort Menu by Price

Reorder the menu from cheapest to most expensive using Java’s Comparator.

5️⃣ Allergy-Sensitive Filter

Type a keyword (like chicken or fries) to hide items containing it.
Perfect for allergies or dietary restrictions.

6️⃣ Mood-Based Recommendations

Tell the system your mood, and it will suggest meals:

Mood	Suggested Meal
hungry	Highest-calorie meal
sad	Spicy meal
healthy	Vegan meal
happy	Combo meal
7️⃣ Auto-Budget Ordering

Enter a budget and see all the meals you can afford.

8️⃣ Admin Mode

For menu management:

➕ Add new items

📝 Edit existing items

❌ Delete items

OOP Principles in Action
💊 Encapsulation

MenuItem keeps its fields private (name, price, calories, category, allergens) and uses getters/setters.
This protects data and ensures controlled updates.



private String name;
private double price;
private int calories;




💡 Abstraction

MenuItem is abstract you can’t create it directly.
It hides implementation details while requiring subclasses to define their own display() method.




abstract class MenuItem {
    public abstract void display();
}




🧬 Inheritance

SingleMeal and ComboMeal inherit from MenuItem, reusing fields and methods.



class SingleMeal extends MenuItem { ... }
class ComboMeal extends MenuItem { ... }




🎭 Polymorphism

Both SingleMeal and ComboMeal override display().
When the system loops through items:




@Override
public void display() {
    System.out.printf("%s | %.2f | %d cal | %s%n",
            getName(), getPrice(), getCalories(), getCategory());
}

@Override
public void display() {
    System.out.printf("%s (Combo) | %.2f | Items: ", getName(), getPrice());
    for (MenuItem item : items) {
        System.out.print(item.getName() + " ");
    }
    System.out.println();
}






…it works seamlessly, regardless of the item type.


Full Code of Donny's Order


import java.util.*;

// Base class
abstract class MenuItem {
    private String name;
    private double price;
    private int calories;
    private String category;
    private List<String> allergens;

    public MenuItem(String name, double price, int calories, String category, List<String> allergens) {
        this.name = name;
        this.price = price;
        this.calories = calories;
        this.category = category;
        this.allergens = allergens;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getCalories() { return calories; }
    public String getCategory() { return category; }
    public List<String> getAllergens() { return allergens; }

    public void setName(String name) { this.name = name; }
    public void setPrice(double price) { this.price = price; }
    public void setCalories(int calories) { this.calories = calories; }
    public void setCategory(String category) { this.category = category; }

    public abstract void display();
}

// Single meal
class SingleMeal extends MenuItem {
    public SingleMeal(String name, double price, int calories, String category, List<String> allergens) {
        super(name, price, calories, category, allergens);
    }

    @Override
    public void display() {
        System.out.printf("%s | %.2f | %d cal | %s%n",
                getName(), getPrice(), getCalories(), getCategory());
    }
}

// Combo meal
class ComboMeal extends MenuItem {
    private List<MenuItem> items;

    public ComboMeal(String name, double price, List<MenuItem> items) {
        super(name, price, 0, "Combo", new ArrayList<>());
        this.items = items;
    }

    @Override
    public void display() {
        System.out.printf("%s (Combo) | %.2f | Items: ", getName(), getPrice());
        for (MenuItem item : items) {
            System.out.print(item.getName() + " ");
        }
        System.out.println();
    }
}

// Order system
class OrderSystem {
    private List<MenuItem> menu = new ArrayList<>();
    private List<MenuItem> cart = new ArrayList<>();
    private Scanner sc = new Scanner(System.in);

    public OrderSystem() {
        seedMenu();
    }

    private void seedMenu() {
        MenuItem burger = new SingleMeal("Classic Burger", 120, 550, "Regular", Arrays.asList("gluten"));
        MenuItem fries = new SingleMeal("French Fries", 60, 300, "Regular", new ArrayList<>());
        MenuItem chicken = new SingleMeal("Fried Chicken", 150, 700, "Spicy", Arrays.asList("soy"));
        MenuItem salad = new SingleMeal("Veggie Salad", 90, 180, "Vegan", new ArrayList<>());

        menu.add(burger);
        menu.add(fries);
        menu.add(chicken);
        menu.add(salad);

        menu.add(new ComboMeal("Burger Combo", 199, Arrays.asList(burger, fries)));
        menu.add(new ComboMeal("Chicken Combo", 249, Arrays.asList(chicken, fries)));
    }

    public void start() {
        while (true) {
            System.out.println("\n==============================");
            System.out.println("       DONNY'S ORDER SYSTEM");
            System.out.println("==============================");
            System.out.println("1. View Menu");
            System.out.println("2. Add to Cart");
            System.out.println("3. View Cart + Receipt");
            System.out.println("4. Sort Menu by Price");
            System.out.println("5. Allergy-Smart Filter");
            System.out.println("6. Mood-Based Recommendation");
            System.out.println("7. Auto-Budget Ordering");
            System.out.println("8. Admin Mode");
            System.out.println("9. Exit");
            System.out.print("Choose: ");

            int choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {
                case 1: showMenu(); break;
                case 2: addToCart(); break;
                case 3: showCart(); break;
                case 4: sortMenu(); break;
                case 5: allergyFilter(); break;
                case 6: moodRecommend(); break;
                case 7: budgetOrder(); break;
                case 8: adminMode(); break;
                case 9: System.out.println("Goodbye!"); return;
                default: System.out.println("Invalid option!");
            }
        }
    }

    private void showMenu() {
        System.out.println("\nMenu:");
        for (int i = 0; i < menu.size(); i++) {
            System.out.print((i + 1) + ". ");
            menu.get(i).display();
        }
        System.out.println("==============================");
    }

    private void addToCart() {
        showMenu();
        System.out.print("Enter item number to add to cart: ");
        int choice = sc.nextInt();
        sc.nextLine();
        if (choice < 1 || choice > menu.size()) {
            System.out.println("Invalid item.");
            return;
        }
        cart.add(menu.get(choice - 1));
        System.out.println("Added to cart!");
    }

    private void showCart() {
        if (cart.isEmpty()) {
            System.out.println("Cart is empty.");
            return;
        }
        double total = 0;
        System.out.println("\nYour Receipt:");
        for (MenuItem i : cart) {
            System.out.printf("• %-20s %.2f%n", i.getName(), i.getPrice());
            total += i.getPrice();
        }
        System.out.printf("Subtotal: %.2f%n", total);

        System.out.print("Are you a student? (yes/no): ");
        String ans = sc.nextLine().toLowerCase();
        if (ans.equals("yes")) {
            double discount = total * 0.10;
            total -= discount;
            System.out.printf("Student Discount (10%%): -%.2f%n", discount);
        }

        System.out.printf("TOTAL: %.2f%n", total);
    }

    private void sortMenu() {
        menu.sort(Comparator.comparingDouble(MenuItem::getPrice));
        System.out.println("Menu sorted by price.");
        showMenu();
    }

    private void allergyFilter() {
        System.out.print("Enter item to avoid (e.g., burger, fries): ");
        String avoidItem = sc.nextLine().toLowerCase();

        System.out.println("Menu excluding " + avoidItem + ":");
        boolean found = false;

        for (MenuItem m : menu) {
            if (!m.getName().toLowerCase().contains(avoidItem)) {
                m.display();
                found = true;
            }
        }
        if (!found) System.out.println("No items available after filter.");
    }

    private void moodRecommend() {
        System.out.print("Your mood (hungry/sad/healthy/happy): ");
        String mood = sc.nextLine().toLowerCase();

        if (mood.equals("hungry"))
            menu.stream().max(Comparator.comparingInt(MenuItem::getCalories)).ifPresent(MenuItem::display);
        else if (mood.equals("sad"))
            menu.stream().filter(m -> m.getCategory().equals("Spicy")).findFirst().ifPresent(MenuItem::display);
        else if (mood.equals("healthy"))
            menu.stream().filter(m -> m.getCategory().equals("Vegan")).findFirst().ifPresent(MenuItem::display);
        else if (mood.equals("happy"))
            menu.stream().filter(m -> m instanceof ComboMeal).findFirst().ifPresent(MenuItem::display);
        else
            System.out.println("No matching mood.");
    }

    private void budgetOrder() {
        System.out.print("Enter your budget: ");
        double budget = sc.nextDouble();
        sc.nextLine();

        System.out.println("Items within your budget:");
        for (MenuItem m : menu)
            if (m.getPrice() <= budget)
                m.display();
    }

    private void adminMode() {
        System.out.println("1. Add Item\n2. Edit Item\n3. Delete Item\nChoose: ");
        int c = sc.nextInt();
        sc.nextLine();

        if (c == 1) addItem();
        else if (c == 2) editItem();
        else if (c == 3) deleteItem();
        else System.out.println("Invalid option!");
    }

    private void addItem() {
        System.out.print("Name: ");
        String name = sc.nextLine();
        System.out.print("Price: ");
        double price = sc.nextDouble();
        sc.nextLine();
        System.out.print("Calories: ");
        int cal = sc.nextInt();
        sc.nextLine();
        System.out.print("Category: ");
        String cat = sc.nextLine();

        menu.add(new SingleMeal(name, price, cal, cat, new ArrayList<>()));
        System.out.println("Item added!");
    }

    private void editItem() {
        showMenu();
        System.out.print("Select item to edit: ");
        int i = sc.nextInt();
        sc.nextLine();

        if (i < 1 || i > menu.size()) return;

        MenuItem m = menu.get(i - 1);

        System.out.print("New Name: ");
        m.setName(sc.nextLine());
        System.out.print("New Price: ");
        m.setPrice(sc.nextDouble());
        sc.nextLine();
        System.out.print("New Calories: ");
        m.setCalories(sc.nextInt());
        sc.nextLine();
        System.out.print("New Category: ");
        m.setCategory(sc.nextLine());

        System.out.println("Item updated!");
    }

    private void deleteItem() {
        showMenu();
        System.out.print("Delete item #: ");
        int i = sc.nextInt();
        sc.nextLine();

        if (i < 1 || i > menu.size()) return;

        menu.remove(i - 1);
        System.out.println("Item deleted!"); 
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        OrderSystem system = new OrderSystem();
        system.start();
    }
}


Example Menu
1. Classic Burger | 120.00 | 550 cal | Regular
2. French Fries | 60.00 | 300 cal | Regular
3. Fried Chicken | 150.00 | 700 cal | Spicy
4. Veggie Salad | 90.00 | 180 cal | Vegan
5. Burger Combo (Combo) | 199.00 | Items: Classic Burger, French Fries
6. Chicken Combo (Combo) | 249.00 | Items: Fried Chicken, French Fries

Example Main Menu
==============================
     DONNY'S ORDER SYSTEM
==============================
1. View Menu
2. Add to Cart
3. View Cart + Receipt
4. Sort Menu by Price
5. Allergy-Smart Filter
6. Mood-Based Recommendation
7. Auto-Budget Ordering
8. Admin Mode
9. Exit
Choose:

Acknowledgments

Big thanks to our instructor for guidance, and to classmates for feedback and support.

Acknowledgments

Big thanks to our instructor for guidance, and to classmates for feedback and support.
