# Expense-tracker-
To accurately outline the scope of work required for a project, it is crucial to first identify itsobjectives. Pinpointing what the project hopes to accomplish will assist in determining itsinclusions and limitations.
Here's a simple expense tracker implementation in Java:



 
Here's a simple expense tracker code in Java using GUI (Graphical User Interface) with Swing library:

ExpenseTracker.java

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

public class ExpenseTracker {
    JFrame frame;
    JTextField dateField, categoryField, amountField;
    JTextArea expenseList;
    JButton addButton, deleteButton, totalButton;
    ArrayList<Expense> expenses;

    public ExpenseTracker() {
        createGUI();
    }

    void createGUI() {
        frame = new JFrame("Expense Tracker");
        frame.setSize(400, 400);
        frame.setLayout(new BorderLayout());
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Input Panel
        JPanel inputPanel = new JPanel();
        inputPanel.setLayout(new GridLayout(3, 2));
        frame.add(inputPanel, BorderLayout.NORTH);

        inputPanel.add(new JLabel("Date (yyyy-mm-dd)"));
        dateField = new JTextField();
        inputPanel.add(dateField);

        inputPanel.add(new JLabel("Category"));
        categoryField = new JTextField();
        inputPanel.add(categoryField);

        inputPanel.add(new JLabel("Amount"));
        amountField = new JTextField();
        inputPanel.add(amountField);

        // Button Panel
        JPanel buttonPanel = new JPanel();
        frame.add(buttonPanel, BorderLayout.CENTER);

        addButton = new JButton("Add Expense");
        addButton.addActionListener(this::addExpense);
        buttonPanel.add(addButton);

        deleteButton = new JButton("Delete Expense");
        deleteButton.addActionListener(this::deleteExpense);
        buttonPanel.add(deleteButton);

        totalButton = new JButton("Total Expenses");
        totalButton.addActionListener(this::calculateTotal);
        buttonPanel.add(totalButton);

        // Expense List
        expenseList = new JTextArea(10, 20);
        frame.add(new JScrollPane(expenseList), BorderLayout.SOUTH);

        expenses = new ArrayList<>();

        frame.setVisible(true);
    }

    void addExpense(ActionEvent e) {
        String date = dateField.getText();
        String category = categoryField.getText();
        double amount = Double.parseDouble(amountField.getText());

        Expense expense = new Expense(date, category, amount);
        expenses.add(expense);

        expenseList.append(expense.toString() + "\n");

        dateField.setText("");
        categoryField.setText("");
        amountField.setText("");
    }

    void deleteExpense(ActionEvent e) {
        int selectedIndex = expenseList.getCaretPosition();
        if (selectedIndex != -1) {
            expenses.remove(selectedIndex / 2);
            expenseList.setText("");
            for (Expense expense : expenses) {
                expenseList.append(expense.toString() + "\n");
            }
        }
    }

    void calculateTotal(ActionEvent e) {
        double total = 0;
        for (Expense expense : expenses) {
            total += expense.getAmount();
        }
        JOptionPane.showMessageDialog(frame, "Total Expenses: " + total);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(ExpenseTracker::new);
    }
}

class Expense {
    private String date;
    private String category;
    private double amount;

    public Expense(String date, String category, double amount) {
        this.date = date;
        this.category = category;
        this.amount = amount;
    }

    public String toString() {
        return date + " - " + category + ": $" + amount;
    }

    public double getAmount() {
        return amount;
    }
}




