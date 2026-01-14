# 📚 JAVA NOTES - CHAPTER 4
## Control Statements

---

### ⭐ Decision Making Statements

🔹 **if Statement**

**Syntax:**
```java
if (condition) {
    // code to execute if condition is true
}
```

**Example:**
```java
int age = 18;
if (age >= 18) {
    System.out.println("You can vote!");
}
```

**Flowchart:**
```
    Start
      ↓
  [Condition]
   /       \
True/       \False
   /         \
  ↓           ↓
[Execute]   [Skip]
  ↓           ↓
   \         /
    \       /
      ↓   ↓
      End
```

---

🔹 **if-else Statement**

**Syntax:**
```java
if (condition) {
    // code if condition is true
} else {
    // code if condition is false
}
```

**Example:**
```java
int marks = 75;
if (marks >= 60) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

**Flowchart:**
```
      Start
        ↓
   [Condition]
    /       \
True/         \False
   /           \
  ↓             ↓
[True Block] [False Block]
  ↓             ↓
   \           /
    \         /
      ↓     ↓
        End
```

---

🔹 **if-else-if Ladder**

**Syntax:**
```java
if (condition1) {
    // code block 1
} else if (condition2) {
    // code block 2
} else if (condition3) {
    // code block 3
} else {
    // default code block
}
```

**Example:**
```java
int marks = 85;
if (marks >= 90) {
    System.out.println("Grade A");
} else if (marks >= 80) {
    System.out.println("Grade B");
} else if (marks >= 70) {
    System.out.println("Grade C");
} else {
    System.out.println("Grade D");
}
```

---

🔹 **switch Statement**

**Syntax:**
```java
switch (expression) {
    case value1:
        // code block 1
        break;
    case value2:
        // code block 2
        break;
    default:
        // default code block
}
```

**Example:**
```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

**⭐ Switch Rules:**
• Expression can be: byte, short, int, char, String, enum
• Each case must have unique value
• `break` statement prevents fall-through
• `default` case is optional but recommended

---

### ⭐ Looping Statements

🔹 **for Loop**

**Syntax:**
```java
for (initialization; condition; increment/decrement) {
    // code to repeat
}
```

**Example:**
```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Number: " + i);
}
```

**Flowchart:**
```
    Start
      ↓
[Initialization]
      ↓
  [Condition] ←─────┐
   /       \       │
True/       \False │
   /         \     │
  ↓           ↓    │
[Loop Body]   End  │
  ↓               │
[Increment]       │
  ↓               │
  └───────────────┘
```

---

🔹 **Enhanced for Loop (for-each)**

**Syntax:**
```java
for (dataType variable : array/collection) {
    // code to execute
}
```

**Example:**
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

---

🔹 **while Loop**

**Syntax:**
```java
while (condition) {
    // code to repeat
}
```

**Example:**
```java
int i = 1;
while (i <= 5) {
    System.out.println("Count: " + i);
    i++;
}
```

**Flowchart:**
```
    Start
      ↓
  [Condition] ←─────┐
   /       \       │
True/       \False │
   /         \     │
  ↓           ↓    │
[Loop Body]   End  │
  ↓               │
  └───────────────┘
```

---

🔹 **do-while Loop**

**Syntax:**
```java
do {
    // code to repeat
} while (condition);
```

**Example:**
```java
int i = 1;
do {
    System.out.println("Count: " + i);
    i++;
} while (i <= 5);
```

**Flowchart:**
```
    Start
      ↓
  [Loop Body]
      ↓
  [Condition]
   /       \
True/       \False
   /         \
  ↓           ↓
  └─────→    End
```

**⭐ Key Difference:**
• `while` - Condition checked first (may not execute)
• `do-while` - Condition checked last (executes at least once)

---

### 🔹 Jump Statements

🔹 **break Statement**
• Exits from loop or switch
• Control goes to statement after loop

```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;  // Exit loop when i = 5
    }
    System.out.println(i);
}
// Output: 1, 2, 3, 4
```

🔹 **continue Statement**
• Skips current iteration
• Control goes to next iteration

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;  // Skip when i = 3
    }
    System.out.println(i);
}
// Output: 1, 2, 4, 5
```

---

### ⭐ Nested Loops

**Example: Multiplication Table**
```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 10; j++) {
        System.out.println(i + " x " + j + " = " + (i*j));
    }
    System.out.println("----------");
}
```

**Pattern Example:**
```java
// Print star pattern
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```
**Output:**
```
* 
* * 
* * * 
* * * * 
* * * * * 
```

---

### 📊 Loop Comparison Table

| Loop Type | When to Use | Entry Condition | Minimum Executions |
|-----------|-------------|-----------------|-------------------|
| for | Known iterations | Checked first | 0 |
| while | Unknown iterations | Checked first | 0 |
| do-while | At least once execution | Checked last | 1 |
| for-each | Array/Collection traversal | Automatic | 0 |

---

### ⭐ Common Programming Patterns

🔹 **Sum of Numbers**
```java
int sum = 0;
for (int i = 1; i <= 10; i++) {
    sum += i;
}
System.out.println("Sum: " + sum);  // 55
```

🔹 **Factorial**
```java
int n = 5, factorial = 1;
for (int i = 1; i <= n; i++) {
    factorial *= i;
}
System.out.println("Factorial: " + factorial);  // 120
```

🔹 **Prime Number Check**
```java
int num = 17;
boolean isPrime = true;
for (int i = 2; i <= num/2; i++) {
    if (num % i == 0) {
        isPrime = false;
        break;
    }
}
```

🔹 **Reverse Number**
```java
int num = 123, reverse = 0;
while (num > 0) {
    reverse = reverse * 10 + num % 10;
    num /= 10;
}
System.out.println("Reverse: " + reverse);  // 321
```

---

### 🔹 Decision Making Flowchart

```
Program Flow Control:

Sequential → Decision → Looping
    ↓           ↓         ↓
 Line by    if/switch   for/while
  Line      statements   loops
    ↓           ↓         ↓
  Next      Branch     Repeat
Statement   based on   until
           condition   condition
                       is false
```

---

**📝 Important Points:**
• Always use braces {} even for single statements
• Avoid infinite loops (ensure condition becomes false)
• Use appropriate loop based on requirement
• `break` exits loop, `continue` skips iteration
• Nested loops increase time complexity
• Use meaningful variable names in loops

---

**⭐ Quick Tips for Exams:**
• Draw flowcharts for complex logic
• Trace through loops with sample values
• Remember loop execution order
• Practice pattern printing programs
• Understand difference between while and do-while

---
*End of Chapter 4* ✅