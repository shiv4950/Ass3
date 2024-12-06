q1
Product.java

public class Product {
    private String name;
    private double price;
    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
    public String getName() {
        return name;
    }
    public double getPrice() {
        return price;
    }
}

q2
TextCalculator.j

public class TaxCalculator {
    private double taxRate;
    public TaxCalculator(double taxRate) {
        this.taxRate = taxRate;
    }
    public double calculateTax(Product product) {
        return product.getPrice() * taxRate;
    }
}

main.java
public class Main {
    public static void main(String[] args) {
        Product product = new Product("Laptop", 1000.00);
        TaxCalculator taxCalculator = new TaxCalculator(0.15);
        double tax = taxCalculator.calculateTax(product);
        System.out.println("Product: " + product.getName());
        System.out.println("Price: $" + product.getPrice());
        System.out.println("Tax: $" + tax);
        System.out.println("Total Price: $" + (product.getPrice() + tax));
    }
}

q2
shape.j
public interface Shape {
    double area();
}

Circle.j
public class Circle implements Shape {
    private double radius;
    public Circle(double radius) {
        this.radius = radius;
    }
    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

public class Rectangle implements Shape {
    private double width;
    private double height;
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    @Override
    public double area() {
        return width * height;
    }
}

public class Triangle implements Shape {
    private double base;
    private double height;
    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }
    @Override
    public double area() {
        return 0.5 * base * height;
    }
}

ShapeCalculator.j
import java.util.List;

public class ShapeCalculator {
    public double totalArea(List<Shape> shapes) {
        double total = 0;
        for (Shape shape : shapes) {
            total += shape.area();
        }
        return total;
    }
}

main.j
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Shape> shapes = new ArrayList<>();
        shapes.add(new Circle(5)); 
        shapes.add(new Rectangle(4, 6)); 
        shapes.add(new Triangle(3, 4)); 
        ShapeCalculator shapeCalculator = new ShapeCalculator();
        double totalArea = shapeCalculator.totalArea(shapes);
        System.out.println("Total Area: " + totalArea);
    }
}


q3
Account.java
public interface Account {
    void deposit(double amount);
    void withdraw(double amount);
    double getBalance();
    double calculateInterest();
}

BaseAccount.j
public abstract class BaseAccount implements Account {
    protected double balance;
    public BaseAccount(double initialBalance) {
        this.balance = initialBalance;
    }
    @Override
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    @Override
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
    @Override
    public double getBalance() {
        return balance;
    }
    public abstract double calculateInterest();
}

SavingsAccount.j
public class SavingsAccount extends BaseAccount {
    private double interestRate;

    public SavingsAccount(double initialBalance, double interestRate) {
        super(initialBalance);
        this.interestRate = interestRate;
    }

    @Override
    public double calculateInterest() {
        return balance * interestRate;
    }
}

main.j
public class Main {
    public static void main(String[] args) {
        Account savingsAccount = new SavingsAccount(1000, 0.05); 
        Account checkingAccount = new CheckingAccount(500, 200); 
        savingsAccount.deposit(200);
        savingsAccount.withdraw(100);
        double savingsInterest = savingsAccount.calculateInterest();
        System.out.println("Savings Account Balance: $" + savingsAccount.getBalance());
        System.out.println("Savings Account Interest: $" + savingsInterest);
        checkingAccount.deposit(300);
        checkingAccount.withdraw(100);
        double checkingInterest = checkingAccount.calculateInterest();
        System.out.println("Checking Account Balance: $" + checkingAccount.getBalance());
        System.out.println("Checking Account Interest: $" + checkingInterest);
    }
}

q4
TaskCreation.j
public interface TaskCreation {
    void createTask(String taskName, String description);
    void deleteTask(String taskId);
}
public interface TaskAssignment {
    void assignTask(String taskId, String assignee);
}
public interface TaskCompletion {
    void markTaskAsComplete(String taskId);
}

TaskCreator.j
public class TaskCreator implements TaskCreation {
    @Override
    public void createTask(String taskName, String description) {
        System.out.println("Task created: " + taskName);
    }
    @Override
    public void deleteTask(String taskId) {
        System.out.println("Task deleted: " + taskId);
    }
}

TaskAssigner.j
public class TaskAssigner implements TaskAssignment {
    @Override
    public void assignTask(String taskId, String assignee) {
        System.out.println("Task " + taskId + " assigned to " + assignee);
    }
}

TaskCompleter.j
public class TaskCompleter implements TaskCompletion {
    @Override
    public void markTaskAsComplete(String taskId) {
        System.out.println("Task " + taskId + " marked as complete");
    }
}
