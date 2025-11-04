Practical Test (Encapsulation, Polymorphism, Public and Private Class, Setter and Getter)
---
This Java program demonstrates the concepts of Object-Oriented Programming (OOP) using encapsulation, inheritance, and polymorphism in a business management system. The Person class serves as the parent class, while Owner, Manager, and Staff inherit its attributes and behaviors. Each subclass overrides the work() method to show polymorphism, where the same method performs differently depending on the object. Encapsulation is implemented through private attributes with getters and setters, ensuring controlled data access. The program also integrates user input, allowing dynamic creation of a business with its owner, manager, and multiple staff members.

Main Class
---
      package MyObject;
      
      import java.util.ArrayList;
      import java.util.Scanner;
      
      public class MainClass {
          public static void main(String[] args) {
              Scanner sc = new Scanner(System.in);
              Business business = new Business();
      
              // === Input Business Name ===
              System.out.print("Enter business name: ");
              business.setName(sc.nextLine());
      
              // === Input Owner Information ===
              System.out.println("\nEnter Owner Information:");
              System.out.print("First Name: ");
              String oFirst = sc.nextLine();
              System.out.print("Middle Name: ");
              String oMiddle = sc.nextLine();
              System.out.print("Last Name: ");
              String oLast = sc.nextLine();
      
              Owner owner = new Owner(oFirst, oMiddle, oLast);
              System.out.print("Business Style: ");
              owner.setBusinessStyle(sc.nextLine());
              business.setOwner(owner);
      
              // === Input Manager Information ===
              System.out.println("\nEnter Manager Information:");
              System.out.print("First Name: ");
              String mFirst = sc.nextLine();
              System.out.print("Middle Name: ");
              String mMiddle = sc.nextLine();
              System.out.print("Last Name: ");
              String mLast = sc.nextLine();
      
              Manager manager = new Manager(mFirst, mMiddle, mLast);
              System.out.print("Department: ");
              manager.setDepartment(sc.nextLine());
              business.setManager(manager);
      
              // === Input Staff Information ===
              ArrayList<Staff> staffList = new ArrayList<>();
              while (true) {
                  System.out.println("\nEnter Staff Information:");
                  System.out.print("First Name: ");
                  String sFirst = sc.nextLine();
                  System.out.print("Middle Name: ");
                  String sMiddle = sc.nextLine();
                  System.out.print("Last Name: ");
                  String sLast = sc.nextLine();
                  System.out.print("Position: ");
                  String position = sc.nextLine();
      
                  Staff staff = new Staff(sFirst, sMiddle, sLast, position);
                  staffList.add(staff);
      
                  // Option to add more staff
                  System.out.print("Add another staff? (y/n): ");
                  String choice = sc.nextLine();
                  if (choice.equalsIgnoreCase("n")) {
                      break;
                  }
              }
              business.setListStaff(staffList);
      
              // === Display Business Information ===
              System.out.println("\n========== BUSINESS INFORMATION ==========");
              System.out.println("Business Name: " + business.getName());
              System.out.println("Owner: " + business.getOwner().fullName());
              System.out.println("Manager: " + business.getManager().fullName());
              System.out.println("\nStaff Members:");
              for (Staff s : business.getListStaff()) {
                  System.out.println("- " + s.fullName() + " (" + s.getPosition() + ")");
              }
      
              // === Demonstrate Polymorphism ===
              System.out.println("\n========== POLYMORPHISM DEMO ==========");
              owner.work(); // Owner’s version of work()
              manager.work(); // Manager’s version of work()
              for (Staff s : business.getListStaff()) {
                  s.work(); // Each Staff’s version of work()
              }
      
              System.out.println("\nProgram has ended. Thank you!");
              sc.close();
          }
      }

Person Class
---
