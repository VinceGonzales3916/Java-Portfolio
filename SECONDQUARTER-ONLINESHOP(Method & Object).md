ONLINE SHOP (Method and OOP)
---
This program is an interactive online shopping system designed using object-oriented programming (OOP) principles and modular methods to improve readability, reusability, and maintainability. The program allows users to browse items, view specifications, select quantity, manage a shopping cart, and proceed to checkout.

Main Class
---
      package MyShopPackage;
      
      import java.util.Scanner;
      
      public class Main {
          public static void main(String[] args) {
              Scanner scanner = new Scanner(System.in);
              Store store = new Store();
              Cart cart = new Cart();
      
              int choice;
              do {
                  System.out.println("\n===== MOBILE STORE MENU =====");
                  System.out.println("1. Shop and Buy");
                  System.out.println("2. Show Cart");
                  System.out.println("3. Checkout");
                  System.out.println("4. Exit");
                  System.out.print("Enter your choice: ");
                  choice = scanner.nextInt();
                  scanner.nextLine();
      
                  switch (choice) {
                      case 1 -> store.shop(cart);
                      case 2 -> cart.showCart();
                      case 3 -> cart.checkout(); // program exits after checkout
                      case 4 -> System.out.println("Thank you for visiting! Exiting program...");
                      default -> System.out.println("Invalid choice. Try again.");
                  }
      
              } while (choice != 4);
      
              scanner.close();
          }
      }

Item Class
---
      package MyShopPackage;
      
      public class Item {
          private String name;
          private String screenSize;
          private String ram;
          private String storage;
          private String os;
          private double price;
      
          public Item(String name, String screenSize, String ram, String storage, String os, double price) {
              this.name = name;
              this.screenSize = screenSize;
              this.ram = ram;
              this.storage = storage;
              this.os = os;
              this.price = price;
          }
      
          // Getters
          public String getName() { return name; }
          public double getPrice() { return price; }
      
          // Display full specs
          public void displaySpecs() {
              System.out.println("\n--- " + name + " ---");
              System.out.println("Screen Size: " + screenSize);
              System.out.println("RAM: " + ram);
              System.out.println("Storage: " + storage);
              System.out.println("Operating System: " + os);
              System.out.println("Price: ₱" + price);
          }
      }

Cart Class
---
      package MyShopPackage;
      
      import java.util.ArrayList;
      import java.util.Scanner;
      
      public class Cart {
          private ArrayList<Item> cartItems = new ArrayList<>();
          private Scanner scanner = new Scanner(System.in);
      
          public void addItem(Item item, int quantity) {
              for (int i = 0; i < quantity; i++) {
                  cartItems.add(item);
              }
              System.out.println(quantity + "x " + item.getName() + " added to cart!");
          }
      
          public void showCart() {
              if (cartItems.isEmpty()) {
                  System.out.println("\nYour cart is empty.");
                  return;
              }
      
              double total = 0;
              System.out.println("\n--- YOUR CART ---");
              for (int i = 0; i < cartItems.size(); i++) {
                  Item item = cartItems.get(i);
                  System.out.println((i + 1) + ". " + item.getName() + " - ₱" + item.getPrice());
                  total += item.getPrice();
              }
              System.out.println("Total: ₱" + total);
      
              System.out.print("\nDo you want to remove an item? (y/n): ");
              String response = scanner.nextLine().trim().toLowerCase();
              if (response.equals("y")) {
                  removeFromCart();
              }
          }
      
          private void removeFromCart() {
              System.out.print("Enter the item number to remove: ");
              int index = scanner.nextInt();
              scanner.nextLine();
              if (index > 0 && index <= cartItems.size()) {
                  Item removed = cartItems.remove(index - 1);
                  System.out.println(removed.getName() + " removed from cart.");
              } else {
                  System.out.println("Invalid choice.");
              }
          }
      
          public double getTotal() {
              double total = 0;
              for (Item item : cartItems) {
                  total += item.getPrice();
              }
              return total;
          }
      
          public void checkout() {
              if (cartItems.isEmpty()) {
                  System.out.println("\nYour cart is empty!");
                  return;
              }
      
              double total = getTotal();
              System.out.println("\nTotal amount due: ₱" + total);
      
              System.out.print("Enter payment amount: ₱");
              double payment = scanner.nextDouble();
              scanner.nextLine();
      
              if (payment >= total) {
                  System.out.println("Payment successful! Change: ₱" + (payment - total));
                  cartItems.clear();
                  System.out.println("Thank you for shopping! Exiting program...");
                  System.exit(0); // Program exits after checkout
              } else {
                  System.out.println("Insufficient payment. Transaction cancelled.");
              }
          }
      
          public boolean isEmpty() {
              return cartItems.isEmpty();
          }
      }

Store Class
---
      package MyShopPackage;
      
      import java.util.ArrayList;
      import java.util.Scanner;
      
      public class Store {
          private ArrayList<Item> storeItems = new ArrayList<>();
          private Scanner scanner = new Scanner(System.in);
      
          public Store() {
              // initialize store items
              storeItems.add(new Item("Samsung Galaxy S24", "6.2-inch", "8GB", "256GB", "Android 14", 57990));
              storeItems.add(new Item("iPhone 15", "6.1-inch", "6GB", "128GB", "iOS 17", 56990));
              storeItems.add(new Item("Oppo Reno11", "6.7-inch", "12GB", "256GB", "Android 14", 24999));
              storeItems.add(new Item("Vivo Y36", "6.64-inch", "8GB", "256GB", "Android 13", 12999));
          }
      
          public void showItems() {
              System.out.println("\n--- AVAILABLE ITEMS ---");
              for (int i = 0; i < storeItems.size(); i++) {
                  System.out.println((i + 1) + ". " + storeItems.get(i).getName() + " - ₱" + storeItems.get(i).getPrice());
              }
          }
      
          public void shop(Cart cart) {
              showItems();
              System.out.print("\nEnter item number to view specs or 0 to go back: ");
              int choice = scanner.nextInt();
              scanner.nextLine();
      
              if (choice > 0 && choice <= storeItems.size()) {
                  Item selected = storeItems.get(choice - 1);
                  selected.displaySpecs();
      
                  System.out.print("\nDo you want to buy this item? (y/n): ");
                  String buy = scanner.nextLine().trim().toLowerCase();
      
                  if (buy.equals("y")) {
                      System.out.print("Enter quantity: ");
                      int qty = scanner.nextInt();
                      scanner.nextLine();
                      cart.addItem(selected, qty);
                  }
              }
          }
      }
