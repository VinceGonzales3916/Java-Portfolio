Classroom Organizer (Encapsulation, Polymorphism, Public and Private Class, Setter and Getter)
---
Main Class
---

      package MyObject;
      
      import java.util.Scanner;
      
      public class myMainClass {
      
          public static void main(String[] args) {
              Scanner scanner = new Scanner(System.in);
      
              // Create section
              Section section = new Section();
              System.out.print("Enter section name: ");
              section.setName(scanner.nextLine());
      
              // Create Teacher
              System.out.println("\nEnter teacher details:");
              System.out.print("First name: ");
              String tFirst = scanner.nextLine();
              System.out.print("Middle name: ");
              String tMiddle = scanner.nextLine();
              System.out.print("Last name: ");
              String tLast = scanner.nextLine();
              System.out.print("Subject: ");
              String subject = scanner.nextLine();
      
              Teacher teacher = new Teacher(tFirst, tMiddle, tLast);
              teacher.setSubject(subject);
              section.setAdviser(teacher);
      
              // Add Students using loop with Y/N option
              String addMore;
              do {
                  System.out.println("\nEnter student details:");
                  System.out.print("First name: ");
                  String sFirst = scanner.nextLine();
                  System.out.print("Middle name: ");
                  String sMiddle = scanner.nextLine();
                  System.out.print("Last name: ");
                  String sLast = scanner.nextLine();
                  System.out.print("Grade: ");
                  int grade = scanner.nextInt();
                  scanner.nextLine(); // consume newline
      
                  Student student = new Student(sFirst, sMiddle, sLast);
                  student.setGrade(grade);
                  section.addStudent(student);
      
                  System.out.print("Do you want to add another student? (y/n): ");
                  addMore = scanner.nextLine().trim().toLowerCase();
      
              } while (addMore.equals("y"));
      
              // Optionally remove a student
              System.out.print("\nDo you want to remove any student? (y/n): ");
              String remove = scanner.nextLine().trim().toLowerCase();
              while (remove.equals("y")) {
                  System.out.print("Enter student number to remove: ");
                  int removeIndex = scanner.nextInt() - 1;
                  scanner.nextLine();
                  section.removeStudent(removeIndex);
      
                  System.out.print("Do you want to remove another student? (y/n): ");
                  remove = scanner.nextLine().trim().toLowerCase();
              }
      
              // Display the section info
              System.out.println("\n===== SECTION DETAILS =====");
              section.displaySection();
      
              scanner.close();
      }
    }

Person Class
---
            package MyObject;
            
            public class Person {
                private int age;
                private String firstName;
                private String middleName;
                private String lastName;
                private String sex;
                private int life = 100;
            
                public Person(String fn, String mn, String ln) {
                    this.firstName = fn;
                    this.middleName = mn;
                    this.lastName = ln;
                }
            
                public Person() {}
            
                // Getters and setters
                public int getAge() { return age; }
                public void setAge(int age) { this.age = age; }
                public String getFirstName() { return firstName; }
                public void setFirstName(String firstName) { this.firstName = firstName; }
                public String getMiddleName() { return middleName; }
                public void setMiddleName(String middleName) { this.middleName = middleName; }
                public String getLastName() { return lastName; }
                public void setLastName(String lastName) { this.lastName = lastName; }
                public String getSex() { return sex; }
                public void setSex(String sex) { this.sex = sex; }
                public int getLife() { return life; }
                public void setLife(int life) { this.life = life; }
            
                // Methods
                public void printName() {
                    System.out.println(firstName + " " + middleName + " " + lastName);
                }
            
                public String fullName() {
                    return firstName + " " + middleName + " " + lastName;
                }
            
                // Polymorphic method
                public void displayInfo() {
                    System.out.println("Name: " + fullName());
                    System.out.println("Age: " + age);
                    System.out.println("Sex: " + sex);
                }
            }
