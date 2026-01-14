# 📚 JAVA NOTES - CHAPTER 6
## Object-Oriented Programming (OOP)

---

### ⭐ What is OOP?

**Object-Oriented Programming** is a programming paradigm based on objects and classes.

🔹 **Key Concepts:**
• Everything is treated as an object
• Objects interact with each other
• Code is organized into classes
• Promotes code reusability and modularity

---

### 🔹 Class and Object

🔹 **Class**
• Blueprint or template for creating objects
• Defines attributes (variables) and methods (functions)
• Does not consume memory until object is created

🔹 **Object**
• Instance of a class
• Real-world entity with state and behavior
• Consumes memory when created

**Syntax:**
```java
class ClassName {
    // Instance variables (attributes)
    dataType variable1;
    dataType variable2;
    
    // Methods (behavior)
    returnType methodName() {
        // method body
    }
}
```

**Example:**
```java
class Student {
    // Instance variables
    String name;
    int age;
    int rollNo;
    
    // Method
    void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Roll No: " + rollNo);
    }
}

// Creating objects
Student s1 = new Student();
s1.name = "John";
s1.age = 20;
s1.rollNo = 101;
s1.displayInfo();
```

---

### 📊 Class vs Object Diagram

```
CLASS (Blueprint)
┌─────────────────────┐
│      Student        │
├─────────────────────┤
│ - name: String      │
│ - age: int          │
│ - rollNo: int       │
├─────────────────────┤
│ + displayInfo()     │
│ + study()           │
└─────────────────────┘
         │
         │ creates
         ↓
OBJECTS (Instances)
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   s1: Student   │  │   s2: Student   │  │   s3: Student   │
├─────────────────┤  ├─────────────────┤  ├─────────────────┤
│ name: "John"    │  │ name: "Alice"   │  │ name: "Bob"     │
│ age: 20         │  │ age: 19         │  │ age: 21         │
│ rollNo: 101     │  │ rollNo: 102     │  │ rollNo: 103     │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

### ⭐ Four Pillars of OOP

### 1. 🔹 Encapsulation

**Definition:** Wrapping data and methods together and hiding internal details

**Key Points:**
• Data hiding using private access modifiers
• Controlled access through public methods (getters/setters)
• Protects data from unauthorized access

**Example:**
```java
class BankAccount {
    private double balance;  // Private data
    
    // Public methods to access private data
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

**Benefits:**
• Data security
• Code maintainability
• Flexibility to change implementation

---

### 2. 🔹 Inheritance

**Definition:** Acquiring properties and methods of parent class by child class

**Syntax:**
```java
class ParentClass {
    // parent class members
}

class ChildClass extends ParentClass {
    // child class members + inherited members
}
```

**Example:**
```java
// Parent class
class Animal {
    String name;
    
    void eat() {
        System.out.println(name + " is eating");
    }
    
    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking");
    }
}

// Usage
Dog d = new Dog();
d.name = "Buddy";
d.eat();    // Inherited method
d.sleep();  // Inherited method
d.bark();   // Own method
```

**Types of Inheritance:**

```
1. Single Inheritance
   A → B

2. Multilevel Inheritance
   A → B → C

3. Hierarchical Inheritance
   A → B
   A → C
   A → D

4. Multiple Inheritance (Not supported in Java)
   A → C ← B

5. Hybrid Inheritance (Not supported in Java)
   Combination of multiple types
```

**Inheritance Hierarchy Diagram:**
```
        Animal (Parent)
       /      |      \
    Dog      Cat     Bird
   /  \       |       |
Puppy GermanShepherd Persian Parrot
```

---

### 3. 🔹 Polymorphism

**Definition:** One interface, multiple implementations (Same method, different behavior)

**Types:**

🔹 **Method Overloading (Compile-time Polymorphism)**
• Same method name, different parameters
• Resolved at compile time

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

🔹 **Method Overriding (Runtime Polymorphism)**
• Same method signature in parent and child class
• Resolved at runtime

```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

// Runtime polymorphism
Animal a1 = new Dog();
Animal a2 = new Cat();
a1.makeSound();  // Dog barks
a2.makeSound();  // Cat meows
```

---

### 4. 🔹 Abstraction

**Definition:** Hiding implementation details and showing only essential features

**Ways to achieve Abstraction:**

🔹 **Abstract Classes**
• Cannot be instantiated
• Can have abstract and concrete methods
• Use `abstract` keyword

```java
abstract class Shape {
    abstract void draw();  // Abstract method
    
    void display() {       // Concrete method
        System.out.println("Displaying shape");
    }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
}
```

🔹 **Interfaces**
• 100% abstraction
• All methods are abstract by default (before Java 8)
• Use `interface` keyword

```java
interface Drawable {
    void draw();  // Abstract method (public abstract by default)
}

class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
}
```

---

### 📊 OOP Relationships Diagram

```
INHERITANCE RELATIONSHIP (IS-A)
┌─────────────┐
│   Vehicle   │
└─────┬───────┘
      │
   ┌──┴──┐
   │ Car │
   └─────┘

COMPOSITION RELATIONSHIP (HAS-A)
┌─────────────┐    ┌─────────────┐
│    Car      │────│   Engine    │
│             │    │             │
└─────────────┘    └─────────────┘

AGGREGATION RELATIONSHIP (USES-A)
┌─────────────┐    ┌─────────────┐
│ Department  │────│  Employee   │
│             │    │             │
└─────────────┘    └─────────────┘
```

---

### ⭐ Access Modifiers

| Modifier | Same Class | Same Package | Subclass | Different Package |
|----------|------------|--------------|----------|-------------------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

---

### 🔹 Constructors

**Definition:** Special method used to initialize objects

**Characteristics:**
• Same name as class
• No return type
• Called automatically when object is created

**Types:**

🔹 **Default Constructor**
```java
class Student {
    String name;
    int age;
    
    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
    }
}
```

🔹 **Parameterized Constructor**
```java
class Student {
    String name;
    int age;
    
    // Parameterized constructor
    Student(String n, int a) {
        name = n;
        age = a;
    }
}

Student s = new Student("John", 20);
```

🔹 **Constructor Overloading**
```java
class Student {
    String name;
    int age;
    
    Student() {
        this("Unknown", 0);
    }
    
    Student(String name) {
        this(name, 0);
    }
    
    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

### 🔹 `this` and `super` Keywords

🔹 **`this` Keyword**
• Refers to current object
• Used to differentiate between instance and local variables
• Call other constructors in same class

```java
class Student {
    String name;
    
    void setName(String name) {
        this.name = name;  // this.name refers to instance variable
    }
    
    Student() {
        this("Default");   // Calls parameterized constructor
    }
    
    Student(String name) {
        this.name = name;
    }
}
```

🔹 **`super` Keyword**
• Refers to parent class object
• Access parent class methods and variables
• Call parent class constructor

```java
class Animal {
    String name;
    
    Animal(String name) {
        this.name = name;
    }
    
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    Dog(String name) {
        super(name);  // Call parent constructor
    }
    
    void eat() {
        super.eat();  // Call parent method
        System.out.println("Dog eats bones");
    }
}
```

---

### ⭐ Complete OOP Example

```java
// Abstract class
abstract class Employee {
    protected String name;
    protected int id;
    protected double salary;
    
    public Employee(String name, int id) {
        this.name = name;
        this.id = id;
    }
    
    // Abstract method
    public abstract void calculateSalary();
    
    // Concrete method
    public void displayInfo() {
        System.out.println("ID: " + id + ", Name: " + name);
    }
}

// Concrete class
class Developer extends Employee {
    private String programmingLanguage;
    
    public Developer(String name, int id, String language) {
        super(name, id);
        this.programmingLanguage = language;
    }
    
    @Override
    public void calculateSalary() {
        salary = 50000;  // Base salary for developer
        System.out.println("Developer salary: " + salary);
    }
}

class Manager extends Employee {
    private int teamSize;
    
    public Manager(String name, int id, int teamSize) {
        super(name, id);
        this.teamSize = teamSize;
    }
    
    @Override
    public void calculateSalary() {
        salary = 70000 + (teamSize * 5000);  // Base + team bonus
        System.out.println("Manager salary: " + salary);
    }
}
```

---

**📝 Important Points:**
• Java supports single inheritance only
• Use `extends` for inheritance, `implements` for interfaces
• Method overriding requires `@Override` annotation
• Abstract classes can have constructors
• Interfaces cannot have constructors
• `private` members are not inherited
• Constructor chaining: child constructor calls parent constructor

---

**⭐ Quick Tips for Exams:**
• Draw inheritance hierarchies for complex problems
• Remember access modifier rules
• Practice method overloading vs overriding
• Understand abstract class vs interface differences
• Know when to use `this` vs `super`
• Practice real-world OOP examples

---
*End of Chapter 6* ✅