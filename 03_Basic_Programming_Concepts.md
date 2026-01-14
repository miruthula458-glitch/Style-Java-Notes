# 📚 JAVA NOTES - CHAPTER 3
## Basic Programming Concepts

---

### ⭐ Data Types in Java

🔹 **Primitive Data Types** (8 types)

| Data Type | Size    | Range                    | Default | Example    |
|-----------|---------|--------------------------|---------|------------|
| byte      | 1 byte  | -128 to 127             | 0       | byte b=10  |
| short     | 2 bytes | -32,768 to 32,767       | 0       | short s=20 |
| int       | 4 bytes | -2³¹ to 2³¹-1           | 0       | int i=100  |
| long      | 8 bytes | -2⁶³ to 2⁶³-1           | 0L      | long l=500L|
| float     | 4 bytes | 6-7 decimal digits      | 0.0f    | float f=3.14f|
| double    | 8 bytes | 15 decimal digits       | 0.0d    | double d=3.14|
| char      | 2 bytes | 0 to 65,535 (Unicode)   | '\u0000'| char c='A' |
| boolean   | 1 bit   | true or false           | false   | boolean b=true|

🔹 **Non-Primitive Data Types**
• String, Arrays, Classes, Interfaces
• Created by programmer
• Can call methods
• Can be null

---

### 🔹 Variables

**Definition:** Container to store data values

**Types of Variables:**

➤ **Local Variables**
• Declared inside methods/blocks
• Must be initialized before use
• Scope limited to method/block

➤ **Instance Variables**
• Declared inside class but outside methods
• Each object has its own copy
• Default values assigned automatically

➤ **Static Variables (Class Variables)**
• Declared with static keyword
• Shared among all objects
• Memory allocated once

**Example:**
```java
class Student {
    static String school = "ABC School";  // Static variable
    String name;                          // Instance variable
    
    void display() {
        int age = 20;                     // Local variable
        System.out.println(name + " " + age);
    }
}
```

---

### ⭐ Variable Declaration Rules

🔹 **Naming Rules:**
• Must start with letter, underscore (_), or dollar ($)
• Cannot start with digit
• Cannot use Java keywords
• Case-sensitive
• No spaces allowed

**Valid Examples:**
• `int age;`
• `String _name;`
• `double $salary;`
• `boolean isActive;`

**Invalid Examples:**
• `int 2age;` ❌ (starts with digit)
• `String class;` ❌ (keyword)
• `double my salary;` ❌ (space)

---

### 🔹 Java Keywords (Reserved Words)

**Total: 53 keywords**

| Category | Keywords |
|----------|----------|
| **Access Modifiers** | public, private, protected |
| **Class Related** | class, interface, extends, implements |
| **Method Related** | void, return, static, final, abstract |
| **Variable Related** | int, float, double, char, boolean, byte, short, long |
| **Control Flow** | if, else, switch, case, default, for, while, do |
| **Exception** | try, catch, finally, throw, throws |
| **Other** | new, this, super, null, true, false |

⭐ **Note:** `goto` and `const` are reserved but not used

---

### ⭐ Operators in Java

🔹 **Arithmetic Operators**
```
+  Addition        5 + 3 = 8
-  Subtraction     5 - 3 = 2
*  Multiplication  5 * 3 = 15
/  Division        5 / 3 = 1 (integer division)
%  Modulus         5 % 3 = 2 (remainder)
```

🔹 **Assignment Operators**
```
=   Simple assignment    a = 5
+=  Add and assign       a += 3  (a = a + 3)
-=  Subtract and assign  a -= 3  (a = a - 3)
*=  Multiply and assign  a *= 3  (a = a * 3)
/=  Divide and assign    a /= 3  (a = a / 3)
%=  Modulus and assign   a %= 3  (a = a % 3)
```

🔹 **Comparison Operators**
```
==  Equal to             5 == 3  → false
!=  Not equal to         5 != 3  → true
>   Greater than         5 > 3   → true
<   Less than            5 < 3   → false
>=  Greater than equal   5 >= 3  → true
<=  Less than equal      5 <= 3  → false
```

🔹 **Logical Operators**
```
&&  Logical AND    (true && false) → false
||  Logical OR     (true || false) → true
!   Logical NOT    (!true) → false
```

🔹 **Unary Operators**
```
++  Increment      a++ or ++a
--  Decrement      a-- or --a
+   Unary plus     +a
-   Unary minus    -a
!   Logical NOT    !a
```

**Pre vs Post Increment:**
```java
int a = 5;
int b = ++a;  // Pre-increment: a=6, b=6
int c = a++;  // Post-increment: c=6, a=7
```

🔹 **Bitwise Operators**
```
&   Bitwise AND     5 & 3 = 1
|   Bitwise OR      5 | 3 = 7
^   Bitwise XOR     5 ^ 3 = 6
~   Bitwise NOT     ~5 = -6
<<  Left shift      5 << 1 = 10
>>  Right shift     5 >> 1 = 2
>>> Unsigned right  5 >>> 1 = 2
```

🔹 **Ternary Operator**
```java
condition ? value1 : value2

int max = (a > b) ? a : b;
// If a > b, max = a, otherwise max = b
```

---

### 📊 Operator Precedence (High to Low)

```
1. () [] .                    (Parentheses, Array, Member access)
2. ++ -- + - ! ~             (Unary operators)
3. * / %                     (Multiplication, Division, Modulus)
4. + -                       (Addition, Subtraction)
5. << >> >>>                 (Shift operators)
6. < <= > >= instanceof      (Relational operators)
7. == !=                     (Equality operators)
8. &                         (Bitwise AND)
9. ^                         (Bitwise XOR)
10. |                        (Bitwise OR)
11. &&                       (Logical AND)
12. ||                       (Logical OR)
13. ?:                       (Ternary operator)
14. = += -= *= /= %=         (Assignment operators)
```

---

### ⭐ Type Casting

🔹 **Implicit Casting (Widening)**
• Automatic conversion
• Smaller to larger data type
• No data loss

```java
int a = 10;
double b = a;  // int to double (automatic)
```

🔹 **Explicit Casting (Narrowing)**
• Manual conversion
• Larger to smaller data type
• Possible data loss

```java
double a = 10.5;
int b = (int) a;  // double to int (manual)
// b = 10 (decimal part lost)
```

**Casting Hierarchy:**
```
byte → short → int → long → float → double
       char  ↗
```

---

### 🔹 Constants in Java

**Using `final` keyword:**
```java
final int MAX_SIZE = 100;
final double PI = 3.14159;
final String COMPANY_NAME = "ABC Corp";
```

**Naming Convention:**
• Use UPPER_CASE with underscores
• Must be initialized when declared
• Cannot be changed after initialization

---

### ⭐ Quick Examples

```java
// Variable declaration and initialization
int age = 25;
String name = "John";
boolean isStudent = true;

// Arithmetic operations
int sum = 10 + 5;      // 15
int diff = 10 - 5;     // 5
int product = 10 * 5;  // 50
int quotient = 10 / 5; // 2
int remainder = 10 % 3; // 1

// Comparison
boolean result = (10 > 5);  // true

// Logical operations
boolean and = (true && false);  // false
boolean or = (true || false);   // true
boolean not = !true;            // false
```

---

**📝 Important Points:**
• Java is strongly typed language
• Variables must be declared before use
• Default values for instance variables only
• Local variables must be initialized
• Use meaningful variable names
• Follow camelCase naming convention

---
*End of Chapter 3* ✅