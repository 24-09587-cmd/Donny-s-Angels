🍔 Donny’s Order System

Your friendly console-based fast-food ordering companion

CS 2106 — Object-oriented Programming

Abaya,Lorien Emmanuel A.

Bacorayo, John Bryner R.

Macuha, Czian Gabriel A.

Soriano, Kurt Frederie L.

**Overview**

Donny’s Order System is a Java console app that lets you explore a restaurant menu, place orders, and manage your cart — all from your terminal!

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

💡 Abstraction

MenuItem is abstract you can’t create it directly.
It hides implementation details while requiring subclasses to define their own display() method.

🧬 Inheritance

SingleMeal and ComboMeal inherit from MenuItem, reusing fields and methods.

🎭 Polymorphism

Both SingleMeal and ComboMeal override display().
When the system loops through items:

item.display();


…it works seamlessly, regardless of the item type.

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
