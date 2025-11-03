#Introduction
 This program is a simple canteen ordering system designed to let users order food and drinks from a menu, apply discounts based on their ID type, 
 and generate a receipt showing their purchases, total cost, discount, payment, and change. 
 
 It follows a step-by-step process from selecting items to final payment, making it easy to simulate how a real canteen cashier transaction works.
---

    package MyJavaPackage; // package name
    import java.util.Scanner; // import Scanner for user input
    public class CanteenOrder {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in); // create Scanner for reading input
        
        // Variables grouped by type for cleaner code
        StringBuilder orderList = new StringBuilder(); // stores all ordered items for receipt
        String confirm, itemName, more, idType; // string variables for user input & descriptions
        int choice, quantity; // numeric variables for menu selection & quantity
        double total = 0.0, discount = 0.0, price, orderCost, finalTotal, payment, change; // money calculations
        boolean ordering = true; // controls ordering loop

        System.out.println("Welcome to the Canteen!"); // greeting

        // Main ordering loop
        while (ordering) {
            // Display menu
            System.out.println("\n========== School Canteen Menu ==========");
            System.out.println("\n0. Cancel Order");
            System.out.println("1. Burger - ₱50"); 
            System.out.println("2. Spaghetti - ₱60"); 
            System.out.println("3. Sandwich - ₱40"); 
            System.out.println("4. Fried Rice & Fried Egg - ₱55"); 
            System.out.println("5. Hotdog - ₱35"); 
            System.out.println("6. Siomai Rice - ₱45"); 
            System.out.println("7. Milk Tea - ₱65"); 
            System.out.println("8. Iced Coffee - ₱55"); 
            System.out.println("9. Bottled Water - ₱20"); 
            System.out.println("10. Soft Drink - ₱30"); 
            System.out.print("Choose your order (0-10): ");
            choice = input.nextInt();
            input.nextLine(); // consume leftover newline

            // Cancel order option
            if (choice == 0) {
                System.out.print("Are you sure you want to Cancel Ordering? (yes/no): ");
                confirm = input.nextLine();
                if (confirm.equalsIgnoreCase("yes")) {
                    ordering = false;
                    break; // exit loop
                } else {
                    continue; // back to menu
                }
            }

            // Ask for quantity
            System.out.print("Enter quantity: ");
            quantity = input.nextInt();
            input.nextLine(); // consume newline

            // Determine item name & price based on choice
            itemName = "";
            switch (choice) {
                case 1: price = 50; itemName = "Burger"; break;
                case 2: price = 60; itemName = "Spaghetti"; break;
                case 3: price = 40; itemName = "Sandwich"; break;
                case 4: price = 55; itemName = "Fried Rice & Fried Egg"; break;
                case 5: price = 35; itemName = "Hotdog"; break;
                case 6: price = 45; itemName = "Siomai Rice"; break;
                case 7: price = 65; itemName = "Milk Tea"; break;
                case 8: price = 55; itemName = "Iced Coffee"; break;
                case 9: price = 20; itemName = "Bottled Water"; break;
                case 10: price = 30; itemName = "Soft Drink"; break;
                default:
                    System.out.println("Invalid choice.");
                    continue; // skip invalid input
            }

            // Calculate cost of this order
            orderCost = price * quantity;
            total += orderCost; // add to running total

            // Save order details to receipt
            orderList.append(quantity + " x " + itemName + " (₱" + String.format("%.2f", price) + " each) = ₱" + String.format("%.2f", orderCost) + "\n");

            // Ask if user wants to order more
            System.out.print("Do you want to order another item? (yes/no): ");
            more = input.nextLine();
            if (more.equalsIgnoreCase("no")) {
                ordering = false;
            }
        }

        // If nothing was ordered
        if (total == 0.0) {
            System.out.println("\nNo items ordered. Thank you!");
            input.close();
            return; // exit program
        }

        // Ask for ID type to determine discount
        System.out.print("Enter your ID type (Student/Teacher/School Personnel/None): ");
        idType = input.nextLine();

        // Apply discount based on ID type
        if (idType.equalsIgnoreCase("Student")) {
            discount = total * 0.10;
            System.out.println("Student Discount: 10% applied.");
        } else if (idType.equalsIgnoreCase("Teacher")) {
            discount = total * 0.05;
            System.out.println("Teacher Discount: 5% applied.");
        } else if (idType.equalsIgnoreCase("School Personnel")) {
            discount = total * 0.03;
            System.out.println("Personnel Discount: 3% applied.");
        } else {
            System.out.println("No discount applied.");
        }

        // Calculate final total
        finalTotal = total - discount;
        if (finalTotal < 0) finalTotal = 0.0;

        // Payment process
        payment = 0.0;
        while (true) {
            System.out.printf("Total to Pay: ₱%.2f\n", finalTotal);
            System.out.print("Enter amount of money to pay (enter 0 to cancel): ₱");
            payment = input.nextDouble();
            input.nextLine(); // consume newline

            if (payment == 0.0) {
                System.out.println("Payment cancelled. Transaction aborted.");
                input.close();
                return;
            }
            if (payment < finalTotal) {
                System.out.printf
               ("Insufficient amount. You still owe ₱%.2f. Please enter full payment or 0 to cancel.\n", 
            		   (finalTotal - payment));
                continue;
            }
            break; // valid payment
        }

        // Calculate change
        change = payment - finalTotal;

        // Print receipt
        System.out.println("\n========== Receipt ==========");
        System.out.println("ID Type: " + idType);
        System.out.println("\nOrders:");
        System.out.print(orderList.toString());
        System.out.printf("\nDiscount Applied: ₱%.2f\n", discount);
        System.out.printf("Total before Discount: ₱%.2f\n", total);
        System.out.printf("Final Total to Pay: ₱%.2f\n", finalTotal);
        System.out.printf("Amount Paid: ₱%.2f\n", payment);
        System.out.printf("Change: ₱%.2f\n", change);

        input.close(); // close scanner
    }
}
