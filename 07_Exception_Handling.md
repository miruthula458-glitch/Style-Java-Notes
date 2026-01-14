# 📚 JAVA NOTES - CHAPTER 7
## Exception Handling

---

### ⭐ What is Exception?

**Exception:** An unwanted or unexpected event that occurs during program execution and disrupts normal flow.

🔹 **Examples:**
• Dividing by zero
• Accessing invalid array index
• File not found
• Network connection failure

**Without Exception Handling:**
Program terminates abnormally ❌

**With Exception Handling:**
Program continues execution gracefully ✅

---

### 🔹 Exception Hierarchy

```
                    Object
                      │
                  Throwable
                 /         \
            Error          Exception
           /     \        /         \
    OutOfMemory  Stack   Runtime    Checked
    Error        Overflow Exception  Exception
                 Error      │           │
                           │           │
                    ArithmeticException IOException
                    NullPointerException ClassNotFoundException
                    ArrayIndexOutOfBounds SQLException
                    NumberFormatException
```

---

### ⭐ Types of Exceptions

### 1. 🔹 Checked Exceptions
• Compile-time exceptions
• Must be handled or declared
• Checked by compiler

**Examples:**
• `IOException`
• `SQLException`
• `ClassNotFoundException`
• `FileNotFoundException`

### 2. 🔹 Unchecked Exceptions (Runtime Exceptions)
• Runtime exceptions
• Not checked by compiler
• Can be handled optionally

**Examples:**
• `ArithmeticException`
• `NullPointerException`
• `ArrayIndexOutOfBoundsException`
• `NumberFormatException`

### 3. 🔹 Errors
• Serious problems that applications should not catch
• Usually indicate system-level issues

**Examples:**
• `OutOfMemoryError`
• `StackOverflowError`
• `VirtualMachineError`

---

### 📊 Exception Types Diagram

```
EXCEPTION CLASSIFICATION

Throwable
├── Error (Unchecked)
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── VirtualMachineError
│
└── Exception
    ├── Checked Exceptions
    │   ├── IOException
    │   ├── SQLException
    │   ├── ClassNotFoundException
    │   └── FileNotFoundException
    │
    └── RuntimeException (Unchecked)
        ├── ArithmeticException
        ├── NullPointerException
        ├── ArrayIndexOutOfBoundsException
        └── NumberFormatException
```

---

### ⭐ Exception Handling Keywords

### 1. 🔹 `try` Block
• Contains code that might throw exception
• Must be followed by catch or finally

```java
try {
    // Risky code
    int result = 10 / 0;
}
```

### 2. 🔹 `catch` Block
• Handles specific exception
• Executed when exception occurs in try block

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero!");
}
```

### 3. 🔹 `finally` Block
• Always executes (whether exception occurs or not)
• Used for cleanup code

```java
try {
    // Code
} catch (Exception e) {
    // Handle exception
} finally {
    System.out.println("This always executes");
}
```

### 4. 🔹 `throw` Keyword
• Manually throw an exception
• Used to create custom exceptions

```java
if (age < 18) {
    throw new IllegalArgumentException("Age must be 18 or above");
}
```

### 5. 🔹 `throws` Keyword
• Declares that method might throw exception
• Used in method signature

```java
public void readFile() throws IOException {
    // Code that might throw IOException
}
```

---

### 🔹 Basic Exception Handling Syntax

```java
try {
    // Code that may throw exception
} catch (ExceptionType1 e1) {
    // Handle ExceptionType1
} catch (ExceptionType2 e2) {
    // Handle ExceptionType2
} finally {
    // Cleanup code (optional)
}
```

---

### ⭐ Exception Handling Examples

### 🔹 Example 1: ArithmeticException
```java
public class DivisionExample {
    public static void main(String[] args) {
        try {
            int a = 10;
            int b = 0;
            int result = a / b;  // This will throw ArithmeticException
            System.out.println("Result: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
            System.out.println("Exception message: " + e.getMessage());
        } finally {
            System.out.println("Division operation completed");
        }
    }
}
```

### 🔹 Example 2: ArrayIndexOutOfBoundsException
```java
public class ArrayExample {
    public static void main(String[] args) {
        try {
            int[] arr = {1, 2, 3, 4, 5};
            System.out.println(arr[10]);  // Invalid index
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Array index out of bounds!");
            System.out.println("Valid indices: 0 to " + (arr.length - 1));
        }
    }
}
```

### 🔹 Example 3: Multiple Catch Blocks
```java
public class MultipleCatchExample {
    public static void main(String[] args) {
        try {
            String str = null;
            System.out.println(str.length());  // NullPointerException
            
            int[] arr = new int[5];
            arr[10] = 50;  // ArrayIndexOutOfBoundsException
            
            int result = 10 / 0;  // ArithmeticException
            
        } catch (NullPointerException e) {
            System.out.println("Null pointer error!");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index error!");
        } catch (ArithmeticException e) {
            System.out.println("Arithmetic error!");
        } catch (Exception e) {  // Generic catch (should be last)
            System.out.println("Some other error occurred!");
        }
    }
}
```

---

### 🔹 `throw` vs `throws`

| `throw` | `throws` |
|---------|----------|
| Used to manually throw exception | Used to declare exception |
| Used inside method body | Used in method signature |
| Followed by exception object | Followed by exception class |
| Can throw only one exception | Can declare multiple exceptions |

**Example:**
```java
// Using throws
public void validateAge(int age) throws IllegalArgumentException {
    if (age < 18) {
        // Using throw
        throw new IllegalArgumentException("Age must be 18 or above");
    }
    System.out.println("Valid age: " + age);
}

public void testAge() {
    try {
        validateAge(15);
    } catch (IllegalArgumentException e) {
        System.out.println("Error: " + e.getMessage());
    }
}
```

---

### ⭐ Custom Exceptions

**Creating Custom Exception:**
```java
// Custom checked exception
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

// Custom unchecked exception
class InsufficientBalanceException extends RuntimeException {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

// Usage
class BankAccount {
    private double balance;
    
    public void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException("Insufficient balance!");
        }
        balance -= amount;
    }
    
    public void setAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or above");
        }
    }
}
```

---

### 🔹 Exception Propagation

**How exceptions propagate up the call stack:**

```java
class ExceptionPropagation {
    void method1() {
        int result = 10 / 0;  // Exception occurs here
    }
    
    void method2() {
        method1();  // Exception propagates to method2
    }
    
    void method3() {
        try {
            method2();  // Exception caught here
        } catch (ArithmeticException e) {
            System.out.println("Exception caught in method3");
        }
    }
}
```

**Call Stack:**
```
method3() → method2() → method1() → Exception
    ↑                                    ↓
Exception caught here ←←←←←←←←←←←←←←←←←←←←←←
```

---

### ⭐ Best Practices

🔹 **Do's:**
• Always handle specific exceptions first
• Use meaningful exception messages
• Clean up resources in finally block
• Log exceptions for debugging
• Create custom exceptions when needed

🔹 **Don'ts:**
• Don't catch Exception (too generic)
• Don't ignore exceptions (empty catch block)
• Don't use exceptions for control flow
• Don't throw exceptions from finally block

**Good Example:**
```java
FileInputStream file = null;
try {
    file = new FileInputStream("data.txt");
    // Process file
} catch (FileNotFoundException e) {
    System.out.println("File not found: " + e.getMessage());
} catch (IOException e) {
    System.out.println("IO error: " + e.getMessage());
} finally {
    if (file != null) {
        try {
            file.close();
        } catch (IOException e) {
            System.out.println("Error closing file");
        }
    }
}
```

---

### 🔹 Try-with-Resources (Java 7+)

**Automatic resource management:**
```java
// Old way
FileInputStream file = null;
try {
    file = new FileInputStream("data.txt");
    // Use file
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (file != null) {
        try {
            file.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// New way (Try-with-resources)
try (FileInputStream file = new FileInputStream("data.txt")) {
    // Use file
    // File automatically closed
} catch (IOException e) {
    e.printStackTrace();
}
```

---

### 📊 Exception Handling Flow

```
Program Execution Flow:

Normal Flow:
try block → Normal execution → finally block → Continue

Exception Flow:
try block → Exception occurs → catch block → finally block → Continue

Unhandled Exception:
try block → Exception occurs → No matching catch → Program terminates
```

---

### ⭐ Common Exception Examples

```java
// 1. NullPointerException
String str = null;
int length = str.length();  // NPE

// 2. ArrayIndexOutOfBoundsException
int[] arr = {1, 2, 3};
int value = arr[5];  // AIOOBE

// 3. NumberFormatException
String text = "abc";
int number = Integer.parseInt(text);  // NFE

// 4. ClassCastException
Object obj = "Hello";
Integer num = (Integer) obj;  // CCE

// 5. IllegalArgumentException
Thread.sleep(-1000);  // IAE (negative sleep time)
```

---

**📝 Important Points:**
• Exception handling doesn't fix the error, it handles it gracefully
• `finally` block executes even if there's a return statement in try/catch
• Checked exceptions must be handled or declared
• Runtime exceptions are optional to handle
• Use specific exception types rather than generic Exception
• Custom exceptions should extend appropriate base class

---

**⭐ Quick Tips for Exams:**
• Remember exception hierarchy
• Know difference between throw and throws
• Practice try-catch-finally combinations
• Understand exception propagation
• Know when to use checked vs unchecked exceptions
• Practice creating custom exceptions

---
*End of Chapter 7* ✅