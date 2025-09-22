import java.util.InputMismatchException;
import java.util.Scanner;

public class Calculator {

    private static double add(double leftOperand, double rightOperand) {
        return leftOperand + rightOperand;
    }

    private static double subtract(double leftOperand, double rightOperand) {
        return leftOperand - rightOperand;
    }

    private static double multiply(double leftOperand, double rightOperand) {
        return leftOperand * rightOperand;
    }

    private static double divide(double leftOperand, double rightOperand) {
        if (rightOperand == 0.0) {
            throw new ArithmeticException("Division by zero is not allowed.");
        }
        return leftOperand / rightOperand;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("==== Basic Calculator ====");
        boolean keepRunning = true;

        while (keepRunning) {
            printMenu();
            System.out.print("Choose an option (1-5): ");
            String choice = scanner.nextLine().trim();

            switch (choice) {
                case "1":
                case "2":
                case "3":
                case "4":
                    Double left = readNumber(scanner, "Enter first number: ");
                    if (left == null) {
                        // invalid input already messaged
                        break;
                    }
                    Double right = readNumber(scanner, "Enter second number: ");
                    if (right == null) {
                        break;
                    }
                    try {
                        double result;
                        if (choice.equals("1")) {
                            result = add(left, right);
                            System.out.println("Result: " + result);
                        } else if (choice.equals("2")) {
                            result = subtract(left, right);
                            System.out.println("Result: " + result);
                        } else if (choice.equals("3")) {
                            result = multiply(left, right);
                            System.out.println("Result: " + result);
                        } else {
                            result = divide(left, right);
                            System.out.println("Result: " + result);
                        }
                    } catch (ArithmeticException ex) {
                        System.out.println("Error: " + ex.getMessage());
                    }
                    break;
                case "5":
                    keepRunning = false;
                    System.out.println("Goodbye!");
                    break;
                default:
                    System.out.println("Invalid option. Please choose between 1 and 5.");
            }
            System.out.println();
        }

        scanner.close();
    }

    private static void printMenu() {
        System.out.println("Select operation:");
        System.out.println("  1) Addition");
        System.out.println("  2) Subtraction");
        System.out.println("  3) Multiplication");
        System.out.println("  4) Division");
        System.out.println("  5) Exit");
    }

    private static Double readNumber(Scanner scanner, String prompt) {
        System.out.print(prompt);
        String line = scanner.nextLine().trim();
        if (line.isEmpty()) {
            System.out.println("Invalid input: empty line.");
            return null;
        }
        try {
            return Double.parseDouble(line);
        } catch (NumberFormatException ex) {
            System.out.println("Invalid number: '" + line + "'. Please try again.");
            return null;
        }
    }
}

