Online Shop (Array Activity)
---
This project is a console-based shopping system developed in Java that simulates the basic functions of an online shopping application. The program allows users to browse a set of available products, add items to their shopping cart, remove items if needed, review the cart, and finally proceed to checkout.

  package MyJavaPackage; // Defines the package name
  
  import java.util.ArrayList; // Imports ArrayList class
  import java.util.Scanner; // Imports Scanner class for input
  
  // Define Item class
  class Item {
      String category; // Item category
      String brand; // Item brand
      double price; // Item price
  
      // Constructor to initialize item
      Item(String category, String brand, double price) {
          this.category = category;
          this.brand = brand;
          this.price = price;
      }
  
      @Override
      public String toString() {
          return category + " - " + brand + " (₱" + price + ")"; // Returns string representation of the item
      }
  }
  
  // Main class
  public class arrayActivity {
  
      public static void main(String[] args) {
          Scanner scanner = new Scanner(System.in); // Scanner object for user input
  
          ArrayList<Item> storeItems = new ArrayList<>(); // List to store available items
          
          // Add laptop items
          storeItems.add(new Item("Laptop", "ASUS", 45000)); 
          storeItems.add(new Item("Laptop", "Acer", 40000));
          storeItems.add(new Item("Laptop", "Lenovo", 42000));
  
          // Add smartphone items
          storeItems.add(new Item("Smartphone", "Samsung", 25000));
          storeItems.add(new Item("Smartphone", "Apple iPhone", 60000));
          storeItems.add(new Item("Smartphone", "Xiaomi", 15000));
  
          // Add headphone items
          storeItems.add(new Item("Headphones", "Sony", 8000));
          storeItems.add(new Item("Headphones", "JBL", 5000));
          storeItems.add(new Item("Headphones", "Beats", 12000));
  
          ArrayList<Item> cart = new ArrayList<>(); // List to store user-selected items
  
          int choice; // Variable to store menu choice
  
          do { // Start of menu loop
              System.out.println("\n==== Online Shopping App ====");
              System.out.println("1. Shop & Buy"); // Option 1: Buy items
              System.out.println("2. Remove from Cart"); // Option 2: Remove item
              System.out.println("3. Show Cart"); // Option 3: Show cart
              System.out.println("4. Checkout"); // Option 4: Checkout
              System.out.println("5. Exit"); // Option 5: Exit program
              System.out.print("Enter your choice: ");
              choice = scanner.nextInt(); // Get user input for menu choice
              scanner.nextLine(); // Consume leftover newline
  
              switch (choice) { // Menu selection
                  case 1:
                      System.out.println("\n--- Available Items ---");
                      for (int i = 0; i < storeItems.size(); i++) { // Display all store items
                          System.out.println((i + 1) + ". " + storeItems.get(i));
                      }
                      System.out.print("Enter the number of the item to buy (0 to cancel): ");
                      int buyIndex = scanner.nextInt() - 1; // User selects item index
  
                      if (buyIndex == -1) { // Cancel selection
                          System.out.println("Returning to menu...");
                      } else if (buyIndex >= 0 && buyIndex < storeItems.size()) { // Valid selection
                          Item selectedItem = storeItems.get(buyIndex);
                          cart.add(selectedItem); // Add to cart
                          System.out.println(selectedItem + " has been added to your cart.");
                          System.out.println("The item was successfully added.");
                      } else { // Invalid selection
                          System.out.println("Invalid item number.");
                      }
                      break;
  
                  case 2:
                      if (cart.isEmpty()) { // Cart is empty
                          System.out.println("\nYour cart is empty.");
                      } else {
                          System.out.println("\nEnter the number of the item to remove:");
                          for (int i = 0; i < cart.size(); i++) { // Display cart items
                              System.out.println((i + 1) + ". " + cart.get(i));
                          }
                          System.out.print("Choice: ");
                          int removeIndex = scanner.nextInt() - 1; // User selects item to remove
  
                          if (removeIndex >= 0 && removeIndex < cart.size()) { // Valid index
                              Item removedItem = cart.remove(removeIndex); // Remove item
                              System.out.println(removedItem + " has been removed from your cart.");
                              System.out.println("The item was successfully removed.");
                          } else { // Invalid index
                              System.out.println("Invalid item number.");
                          }
                      }
                      break;
  
                  case 3:
                      System.out.println("\n--- Your Shopping Cart ---");
                      if (cart.isEmpty()) { // Cart empty
                          System.out.println("Your cart is empty.");
                      } else {
                          double total = 0; // Initialize total price
                          for (int i = 0; i < cart.size(); i++) { // Display cart items
                              System.out.println((i + 1) + ". " + cart.get(i));
                              total += cart.get(i).price; // Sum total
                          }
                          System.out.println("Total: ₱" + total); // Show total
                      }
                      break;
  
                  case 4:
                      if (cart.isEmpty()) { // Cart empty
                          System.out.println("\nYour cart is empty. Add items before checkout.");
                      } else {
                          System.out.println("\n--- Checkout ---");
                          double total = 0; // Initialize total
                          for (int i = 0; i < cart.size(); i++) { // Display cart items
                              System.out.println((i + 1) + ". " + cart.get(i));
                              total += cart.get(i).price; // Sum total
                          }
                          System.out.println("Total Amount: ₱" + total);
  
                          double payment; // Payment amount
                          do { // Loop until sufficient payment
                              System.out.print("Enter payment amount: ₱");
                              payment = scanner.nextDouble();
  
                              if (payment < total) { // Insufficient payment
                                  System.out.println("Insufficient payment. Please enter at least ₱" + total);
                              } else { // Payment sufficient
                                  double change = payment - total; // Calculate change
                                  if (change > 0) { // If change exists
                                      System.out.println("Payment accepted. Your change is ₱" + change);
                                  } else { // Exact payment
                                      System.out.println("Payment accepted. Exact amount received.");
                                  }
                                  System.out.println("Thank you for your purchase!");
                                  cart.clear(); // Clear cart after checkout
                              }
                          } while (payment < total); // Repeat if payment insufficient
                      }
                      break;
  
                  case 5:
                      System.out.println("Thank you for visiting! Exiting program..."); // Exit message
                      break;
  
                  default:
                      System.out.println("Invalid choice. Please try again."); // Invalid menu option
              }
  
          } while (choice != 5); // Repeat menu until exit
  
          scanner.close(); // Close scanner
      }
  }

