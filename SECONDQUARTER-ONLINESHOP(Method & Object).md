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
                      case 3 -> cart.checkout();
                      case 4 -> System.out.println("Thank you for visiting! Exiting program...");
                      default -> System.out.println("Invalid choice. Try again.");
                  }
      
              } while (choice != 4);
      
              scanner.close();
          }
      }
