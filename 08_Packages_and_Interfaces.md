# 📚 JAVA NOTES - CHAPTER 8
## Packages and Interfaces

---

### ⭐ Packages in Java

**Package:** A namespace that organizes related classes and interfaces

🔹 **Benefits:**
• Organize related classes
• Avoid naming conflicts
• Control access with access modifiers
• Easy to locate and use classes
• Provide controlled access

---

### 🔹 Types of Packages

### 1. **Built-in Packages (Java API)**
• Pre-defined packages provided by Java
• Ready to use in programs

**Common Built-in Packages:**

| Package | Description | Common Classes |
|---------|-------------|----------------|
| `java.lang` | Fundamental classes | String, Object, System, Math |
| `java.util` | Utility classes | ArrayList, HashMap, Scanner |
| `java.io` | Input/Output classes | FileInputStream, BufferedReader |
| `java.net` | Networking classes | URL, Socket, ServerSocket |
| `java.awt` | GUI components | Button, Frame, Panel |
| `java.sql` | Database connectivity | Connection, Statement, ResultSet |
| `javax.swing` | Advanced GUI | JFrame, JButton, JTextField |

### 2. **User-defined Packages**
• Created by programmer
• Custom organization of classes

---

### 🔹 Creating and Using Packages

### **Creating a Package:**

**Step 1:** Create package structure
```
myproject/
├── com/
│   └── company/
│       └── utils/
│           ├── Calculator.java
│           └── StringHelper.java
└── Main.java
```

**Step 2:** Declare package in Java file
```java
// File: com/company/utils/Calculator.java
package com.company.utils;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int subtract(int a, int b) {
        return a - b;
    }
}
```

```java
// File: com/company/utils/StringHelper.java
package com.company.utils;

public class StringHelper {
    public String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
    
    public boolean isPalindrome(String str) {
        return str.equals(reverse(str));
    }
}
```

**Step 3:** Use package in other classes
```java
// File: Main.java
import com.company.utils.Calculator;
import com.company.utils.StringHelper;

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println("Sum: " + calc.add(10, 20));
        
        StringHelper helper = new StringHelper();
        System.out.println("Reverse: " + helper.reverse("hello"));
    }
}
```

---

### 🔹 Import Statements

### **Types of Import:**

🔹 **Specific Import**
```java
import java.util.ArrayList;
import java.util.HashMap;
```

🔹 **Wildcard Import**
```java
import java.util.*;  // Imports all classes from java.util
```

🔹 **Static Import**
```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

// Now can use PI and sqrt directly
double area = PI * radius * radius;
double result = sqrt(16);
```

🔹 **Fully Qualified Name (No Import)**
```java
java.util.ArrayList<String> list = new java.util.ArrayList<>();
```

---

### 📊 Package Structure Diagram

```
Java Package Hierarchy:

java (root package)
├── lang (automatically imported)
│   ├── String
│   ├── Object
│   ├── System
│   └── Math
├── util
│   ├── ArrayList
│   ├── HashMap
│   ├── Scanner
│   └── Date
├── io
│   ├── FileInputStream
│   ├── FileOutputStream
│   └── BufferedReader
└── net
    ├── URL
    ├── Socket
    └── ServerSocket

Custom Package Example:
com.company.project
├── model
│   ├── User.java
│   └── Product.java
├── service
│   ├── UserService.java
│   └── ProductService.java
└── util
    ├── DatabaseHelper.java
    └── ValidationHelper.java
```

---

### ⭐ Interfaces in Java

**Interface:** A contract that defines what a class must do, but not how it does it

🔹 **Characteristics:**
• 100% abstraction (before Java 8)
• All methods are public and abstract by default
• All variables are public, static, and final
• Cannot be instantiated
• Supports multiple inheritance

---

### 🔹 Interface Syntax

```java
interface InterfaceName {
    // Constants (public static final by default)
    int CONSTANT_VALUE = 100;
    
    // Abstract methods (public abstract by default)
    void method1();
    int method2(String param);
    
    // Default methods (Java 8+)
    default void defaultMethod() {
        System.out.println("Default implementation");
    }
    
    // Static methods (Java 8+)
    static void staticMethod() {
        System.out.println("Static method in interface");
    }
}
```

---

### 🔹 Interface Implementation

```java
// Interface definition
interface Drawable {
    void draw();
    void resize(int width, int height);
}

// Class implementing interface
class Circle implements Drawable {
    private int radius;
    
    @Override
    public void draw() {
        System.out.println("Drawing a circle with radius: " + radius);
    }
    
    @Override
    public void resize(int width, int height) {
        this.radius = Math.min(width, height) / 2;
    }
}

class Rectangle implements Drawable {
    private int width, height;
    
    @Override
    public void draw() {
        System.out.println("Drawing rectangle: " + width + "x" + height);
    }
    
    @Override
    public void resize(int width, int height) {
        this.width = width;
        this.height = height;
    }
}
```

---

### 🔹 Multiple Interface Implementation

```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// Class implementing multiple interfaces
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}
```

---

### 🔹 Interface Inheritance

```java
// Base interface
interface Animal {
    void eat();
}

// Extended interface
interface Mammal extends Animal {
    void breathe();
}

// Multiple interface inheritance
interface Flyable {
    void fly();
}

interface Bird extends Animal, Flyable {
    void layEggs();
}

// Implementation
class Eagle implements Bird {
    @Override
    public void eat() {
        System.out.println("Eagle eats fish");
    }
    
    @Override
    public void fly() {
        System.out.println("Eagle flies high");
    }
    
    @Override
    public void layEggs() {
        System.out.println("Eagle lays eggs");
    }
}
```

---

### ⭐ Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| **Keyword** | `abstract class` | `interface` |
| **Implementation** | Can have abstract and concrete methods | All methods abstract (before Java 8) |
| **Variables** | Any type of variables | Only public static final |
| **Inheritance** | Single inheritance | Multiple inheritance |
| **Constructor** | Can have constructors | Cannot have constructors |
| **Access Modifiers** | Any access modifier | Public by default |
| **When to use** | IS-A relationship | CAN-DO relationship |

**Example:**
```java
// Abstract class - IS-A relationship
abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    public void start() {
        System.out.println(brand + " is starting");
    }
    
    public abstract void move();
}

// Interface - CAN-DO relationship
interface Honkable {
    void honk();
}

class Car extends Vehicle implements Honkable {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void move() {
        System.out.println("Car is moving on road");
    }
    
    @Override
    public void honk() {
        System.out.println("Car is honking: Beep beep!");
    }
}
```

---

### 🔹 Java 8+ Interface Features

### **Default Methods:**
```java
interface Calculator {
    int add(int a, int b);
    
    // Default method
    default int multiply(int a, int b) {
        return a * b;
    }
}

class SimpleCalculator implements Calculator {
    @Override
    public int add(int a, int b) {
        return a + b;
    }
    
    // multiply() method is inherited from interface
}
```

### **Static Methods:**
```java
interface MathUtils {
    static double PI = 3.14159;
    
    static double circleArea(double radius) {
        return PI * radius * radius;
    }
}

// Usage
double area = MathUtils.circleArea(5.0);
```

### **Functional Interfaces (Java 8):**
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

// Lambda expression
Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;

System.out.println(add.calculate(5, 3));      // 8
System.out.println(multiply.calculate(5, 3)); // 15
```

---

### 📊 Interface Hierarchy Example

```
Interface Inheritance:

        Drawable
           │
    ┌──────┼──────┐
    │      │      │
Resizable Shape  Colorable
    │      │      │
    └──────┼──────┘
           │
      AdvancedShape
           │
    ┌──────┼──────┐
    │      │      │
  Circle Square Triangle
```

---

### ⭐ Real-World Interface Examples

### **Example 1: Payment System**
```java
interface PaymentProcessor {
    boolean processPayment(double amount);
    void sendReceipt(String email);
}

class CreditCardProcessor implements PaymentProcessor {
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing credit card payment: $" + amount);
        return true;
    }
    
    @Override
    public void sendReceipt(String email) {
        System.out.println("Credit card receipt sent to: " + email);
    }
}

class PayPalProcessor implements PaymentProcessor {
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing PayPal payment: $" + amount);
        return true;
    }
    
    @Override
    public void sendReceipt(String email) {
        System.out.println("PayPal receipt sent to: " + email);
    }
}
```

### **Example 2: Database Operations**
```java
interface DatabaseOperations {
    void connect();
    void disconnect();
    boolean executeQuery(String query);
}

class MySQLDatabase implements DatabaseOperations {
    @Override
    public void connect() {
        System.out.println("Connected to MySQL database");
    }
    
    @Override
    public void disconnect() {
        System.out.println("Disconnected from MySQL database");
    }
    
    @Override
    public boolean executeQuery(String query) {
        System.out.println("Executing MySQL query: " + query);
        return true;
    }
}
```

---

### 🔹 Package Access Control

```java
// File: com/example/model/User.java
package com.example.model;

public class User {
    public String name;        // Accessible everywhere
    protected int age;         // Accessible in package and subclasses
    String email;             // Package-private (default)
    private String password;   // Only within this class
    
    public String getName() {
        return name;
    }
    
    // Package-private method
    void updateEmail(String newEmail) {
        this.email = newEmail;
    }
}
```

---

**📝 Important Points:**
• Package names should be in lowercase
• Use reverse domain naming convention (com.company.project)
• `java.lang` package is automatically imported
• Interface methods are public by default
• A class can implement multiple interfaces
• Interfaces support multiple inheritance
• Use interfaces for contracts, abstract classes for shared code

---

**⭐ Quick Tips for Exams:**
• Remember package naming conventions
• Know difference between import types
• Understand interface vs abstract class
• Practice multiple interface implementation
• Know Java 8+ interface features
• Remember access modifier rules in packages
• Practice real-world interface examples

---
*End of Chapter 8* ✅