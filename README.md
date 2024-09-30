# Expense-tracker-
To accurately outline the scope of work required for a project, it is crucial to first identify itsobjectives. Pinpointing what the project hopes to accomplish will assist in determining itsinclusions and limitations.
Here's a simple expense tracker implementation in Java:


ExpenseTracker.java

import java.util.ArrayList;
import java.util.Scanner;

public class ExpenseTracker {
    private ArrayList<Expense> expenses;
    private double totalExpense;

    public ExpenseTracker() {
        expenses = new ArrayList<>();
        totalExpense = 0.0;
    }

    public void addExpense(String category, double amount) {
        Expense expense = new Expense(category, amount);
        expenses.add(expense);
        totalExpense += amount;
    }

    public void removeExpense(int index) {
        if (index >= 0 && index < expenses.size()) {
            totalExpense -= expenses.get(index).getAmount();
            expenses.remove(index);
        }
    }

    public void displayExpenses() {
        System.out.println("Expenses:");
        for (int i = 0; i < expenses.size(); i++) {
            System.out.println((i + 1) + ". " + expenses.get(i).toString());
        }
        System.out.println("Total Expense: $" + totalExpense);
    }

    public static void main(String[] args) {
        ExpenseTracker tracker = new ExpenseTracker();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Add Expense");
            System.out.println("2. Remove Expense");
            System.out.println("3. Display Expenses");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int option = scanner.nextInt();
            scanner.nextLine(); // Consume newline left-over

            switch (option) {
                case 1:
                    System.out.print("Enter category: ");
                    String category = scanner.nextLine();
                    System.out.print("Enter amount: $");
                    double amount = scanner.nextDouble();
                    scanner.nextLine(); // Consume newline left-over
                    tracker.addExpense(category, amount);
                    break;
                case 2:
                    System.out.print("Enter expense number to remove: ");
                    int index = scanner.nextInt();
                    scanner.nextLine(); // Consume newline left-over
                    tracker.removeExpense(index - 1);
                    break;
                case 3:
                    tracker.displayExpenses();
                    break;
                case 4:
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid option");
            }
        }
    }
}

class Expense {
    private String category;
    private double amount;

    public Expense(String category, double amount) {
        this.category = category;
        this.amount = amount;
    }

    public String getCategory() {
        return category;
    }

    public double getAmount() {
        return amount;
    }

    @Override
    public String toString() {
        return category + " - $" + amount;
    }
}





