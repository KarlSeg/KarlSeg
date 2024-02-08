import java.util.Scanner;

class BankAccFinount {
    private int id;
    private int pin;
    private String name;
    private double balance;

    // Constructor
    public void BankAccount(int id, int pin, String name, double balance) {
        this.id = id;
        this.pin = pin;
        this.name = name;
        this.balance = balance;
    }

    // Getter methods
    public int getId() {
        return id;
    }

    public int getPin() {
        return pin;
    }

    public String getName() {
        return name;
    }

    public double getBalance() {
        return balance;
    }

    // Method to transfer money
    public void transfer(BankAccount recipient, double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            recipient.balance += amount;  // Directly adding to the recipient's balance for simplicity
            System.out.println("Transferred $" + amount + " to " + recipient.getName());
        } else {
            System.out.println("Invalid transfer amount or insufficient funds.");
        }
    }
}

public class FinalOutput {
    public static void main(String[] args) {
        // Create instances of BankAccount
        BankAccount account1 = new BankAccount(412435, 7452, "Chris Sandoval", 32000);
        BankAccount account2 = new BankAccount(264863, 1349, "Marc Yim", 1000);

        // Scanner for user input
        Scanner scanner = new Scanner(System.in);

        // Login
        System.out.print("Enter your user ID: ");
        int userId = scanner.nextInt();
        System.out.print("Enter your PIN: ");
        int pin = scanner.nextInt();

        BankAccount currentUser = null;

        // Validate login credentials
        if (userId == account1.getId() && pin == account1.getPin()) {
            currentUser = account1;
        } else if (userId == account2.getId() && pin == account2.getPin()) {
            currentUser = account2;
        } else {
            System.out.println("Invalid credentials. Exiting...");
            System.exit(0);
        }

        // Transfer money
        System.out.print("Enter recipient's user ID: ");
        int recipientId = scanner.nextInt();
        BankAccount recipient = (recipientId == account1.getId()) ? account1 : account2;

        System.out.print("Enter transfer amount: $");
        double transferAmount = scanner.nextDouble();

        // Perform cash transfer
        currentUser.transfer(recipient, transferAmount);

        // Display updated balances
        System.out.println("Updated balances:");
        System.out.println(currentUser.getName() + ": $" + currentUser.getBalance());
        System.out.println(recipient.getName() + ": $" + recipient.getBalance());

        // Close the scanner
        scanner.close();
    }
}
