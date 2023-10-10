import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Scanner;

class Student {
    private String name;
    private double grade;

    public Student(String name, double grade) {
        this.name = name;
        this.grade = grade;
    }

    public double getGrade() {
        return grade;
    }

    @Override
    public String toString() {
        return name + ": " + grade;
    }
}

Main{
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Student> students = new ArrayList<>();

        while (true) {
            System.out.println("Options:");
            System.out.println("1. Enter student grade");
            System.out.println("2. Calculate average grade");
            System.out.println("3. Categorize grades");
            System.out.println("4. Show top-performing students");
            System.out.println("5. Quit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter student name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter student grade: ");
                    double grade = scanner.nextDouble();
                    students.add(new Student(name, grade));
                    break;

                case 2:
                    double sum = 0;
                    for (Student student : students) {
                        sum += student.getGrade();
                    }
                    double average = sum / students.size();
                    System.out.println("Average grade: " + average);
                    break;

                case 3:
                    for (Student student : students) {
                        System.out.print(student + " - ");
                        if (student.getGrade() >= 90) {
                            System.out.println("A");
                        } else if (student.getGrade() >= 80) {
                            System.out.println("B");
                        } else if (student.getGrade() >= 70) {
                            System.out.println("C");
                        } else if (student.getGrade() >= 60) {
                            System.out.println("D");
                        } else {
                            System.out.println("F");
                        }
                    }
                    break;

                case 4:
                    Collections.sort(students, Comparator.comparingDouble(Student::getGrade).reversed());
                    System.out.println("Top-performing students:");
                    int count = 0;
                    for (Student student : students) {
                        if (count < 3) {
                            System.out.println(student);
                            count++;
                        } else {
                            break;
                        }
                    }
                    break;

                case 5:
                    System.out.println("Goodbye!");
                    scanner.close();
                    System.exit(0);

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
