# 📚 JAVA NOTES - CHAPTER 5
## Arrays and Strings

---

### ⭐ Arrays in Java

**Definition:** Collection of similar data types stored in contiguous memory locations

🔹 **Characteristics:**
• Fixed size (cannot be changed after creation)
• Elements accessed using index (0-based)
• All elements must be of same data type
• Reference type in Java

---

### 🔹 One-Dimensional Arrays

**Declaration:**
```java
// Method 1
int[] arr;
int arr[];

// Method 2 (with size)
int[] arr = new int[5];

// Method 3 (with initialization)
int[] arr = {1, 2, 3, 4, 5};
int[] arr = new int[]{1, 2, 3, 4, 5};
```

**Example:**
```java
// Declaration and initialization
int[] numbers = new int[5];
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
numbers[3] = 40;
numbers[4] = 50;

// Direct initialization
int[] marks = {85, 90, 78, 92, 88};
```

**Array Operations:**
```java
int[] arr = {10, 20, 30, 40, 50};

// Access elements
System.out.println(arr[0]);  // 10
System.out.println(arr[2]);  // 30

// Array length
System.out.println(arr.length);  // 5

// Traverse array
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// Enhanced for loop
for (int element : arr) {
    System.out.println(element);
}
```

---

### 🔹 Two-Dimensional Arrays

**Declaration:**
```java
// Method 1
int[][] matrix;

// Method 2 (with size)
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

// Method 3 (with initialization)
int[][] matrix = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

**Example:**
```java
// 3x3 matrix
int[][] matrix = new int[3][3];

// Initialize values
matrix[0][0] = 1;  matrix[0][1] = 2;  matrix[0][2] = 3;
matrix[1][0] = 4;  matrix[1][1] = 5;  matrix[1][2] = 6;
matrix[2][0] = 7;  matrix[2][1] = 8;  matrix[2][2] = 9;

// Traverse 2D array
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

**Output:**
```
1 2 3 
4 5 6 
7 8 9 
```

---

### ⭐ Array Memory Representation

```
1D Array: arr = {10, 20, 30, 40, 50}

Memory Layout:
Index:  [0] [1] [2] [3] [4]
Value:  10  20  30  40  50
Address: 100 104 108 112 116

2D Array: matrix = {{1,2,3}, {4,5,6}}

Memory Layout:
matrix[0] → [1] [2] [3]
matrix[1] → [4] [5] [6]
```

---

### 🔹 Common Array Operations

🔹 **Finding Maximum Element**
```java
int[] arr = {45, 23, 78, 12, 67};
int max = arr[0];
for (int i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
System.out.println("Maximum: " + max);  // 78
```

🔹 **Array Sum**
```java
int[] arr = {10, 20, 30, 40, 50};
int sum = 0;
for (int element : arr) {
    sum += element;
}
System.out.println("Sum: " + sum);  // 150
```

🔹 **Linear Search**
```java
int[] arr = {10, 20, 30, 40, 50};
int target = 30;
int index = -1;

for (int i = 0; i < arr.length; i++) {
    if (arr[i] == target) {
        index = i;
        break;
    }
}
System.out.println("Found at index: " + index);  // 2
```

🔹 **Array Reversal**
```java
int[] arr = {1, 2, 3, 4, 5};
int n = arr.length;

for (int i = 0; i < n/2; i++) {
    int temp = arr[i];
    arr[i] = arr[n-1-i];
    arr[n-1-i] = temp;
}
// Result: {5, 4, 3, 2, 1}
```

---

### ⭐ Strings in Java

**Definition:** Sequence of characters treated as an object

🔹 **String Characteristics:**
• Immutable (cannot be changed)
• Reference type
• Stored in String Pool (Heap memory)
• Implements CharSequence interface

---

### 🔹 String Creation

```java
// Method 1: String literal
String str1 = "Hello";

// Method 2: Using new keyword
String str2 = new String("Hello");

// Method 3: From character array
char[] chars = {'H', 'e', 'l', 'l', 'o'};
String str3 = new String(chars);
```

**String Pool Concept:**
```java
String s1 = "Hello";        // Stored in String Pool
String s2 = "Hello";        // Points to same object in pool
String s3 = new String("Hello");  // Creates new object in heap

System.out.println(s1 == s2);     // true (same reference)
System.out.println(s1 == s3);     // false (different reference)
System.out.println(s1.equals(s3)); // true (same content)
```

---

### 🔹 Important String Methods

| Method | Description | Example |
|--------|-------------|---------|
| `length()` | Returns string length | `"Hello".length()` → 5 |
| `charAt(index)` | Character at index | `"Hello".charAt(1)` → 'e' |
| `substring(start)` | Substring from start | `"Hello".substring(2)` → "llo" |
| `substring(start,end)` | Substring from start to end-1 | `"Hello".substring(1,4)` → "ell" |
| `indexOf(char)` | First occurrence index | `"Hello".indexOf('l')` → 2 |
| `lastIndexOf(char)` | Last occurrence index | `"Hello".lastIndexOf('l')` → 3 |
| `toLowerCase()` | Convert to lowercase | `"Hello".toLowerCase()` → "hello" |
| `toUpperCase()` | Convert to uppercase | `"Hello".toUpperCase()` → "HELLO" |
| `trim()` | Remove leading/trailing spaces | `" Hello ".trim()` → "Hello" |
| `replace(old,new)` | Replace characters | `"Hello".replace('l','x')` → "Hexxo" |
| `equals(str)` | Compare content | `"Hello".equals("Hello")` → true |
| `equalsIgnoreCase(str)` | Compare ignoring case | `"Hello".equalsIgnoreCase("HELLO")` → true |
| `compareTo(str)` | Lexicographic comparison | `"abc".compareTo("def")` → negative |
| `contains(str)` | Check if contains substring | `"Hello".contains("ell")` → true |
| `startsWith(str)` | Check if starts with | `"Hello".startsWith("He")` → true |
| `endsWith(str)` | Check if ends with | `"Hello".endsWith("lo")` → true |
| `split(delimiter)` | Split into array | `"a,b,c".split(",")` → ["a","b","c"] |

---

### ⭐ String Examples

🔹 **String Concatenation**
```java
String first = "Hello";
String second = "World";

// Method 1: Using + operator
String result1 = first + " " + second;  // "Hello World"

// Method 2: Using concat() method
String result2 = first.concat(" ").concat(second);  // "Hello World"
```

🔹 **String Comparison**
```java
String s1 = "Java";
String s2 = "java";
String s3 = "Java";

System.out.println(s1.equals(s2));           // false
System.out.println(s1.equals(s3));           // true
System.out.println(s1.equalsIgnoreCase(s2)); // true
System.out.println(s1 == s3);                // true (string pool)
```

🔹 **String Manipulation**
```java
String text = "  Java Programming  ";

System.out.println(text.length());           // 19
System.out.println(text.trim().length());    // 16
System.out.println(text.toUpperCase());      // "  JAVA PROGRAMMING  "
System.out.println(text.substring(2, 6));    // "Java"
System.out.println(text.indexOf("Pro"));     // 7
System.out.println(text.replace("Java", "Python")); // "  Python Programming  "
```

---

### 🔹 StringBuilder and StringBuffer

**Problem with String:** Immutable nature creates new objects

**Solution:** Use StringBuilder or StringBuffer

🔹 **StringBuilder (Not Thread-Safe, Faster)**
```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");        // "Hello World"
sb.insert(5, " Java");      // "Hello Java World"
sb.delete(5, 10);          // "Hello World"
sb.reverse();              // "dlroW olleH"

String result = sb.toString();
```

🔹 **StringBuffer (Thread-Safe, Slower)**
```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World");
String result = sb.toString();
```

**Key Methods:**
• `append(str)` - Add at end
• `insert(index, str)` - Insert at position
• `delete(start, end)` - Delete characters
• `reverse()` - Reverse string
• `toString()` - Convert to String

---

### 📊 String vs StringBuilder vs StringBuffer

| Feature | String | StringBuilder | StringBuffer |
|---------|--------|---------------|--------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread Safety | Yes | No | Yes |
| Performance | Slow | Fast | Medium |
| Memory | More | Less | Less |
| Use Case | Few operations | Many operations | Concurrent access |

---

### ⭐ Common String Programs

🔹 **Palindrome Check**
```java
String str = "madam";
String reversed = new StringBuilder(str).reverse().toString();
boolean isPalindrome = str.equals(reversed);
System.out.println(isPalindrome);  // true
```

🔹 **Count Vowels**
```java
String str = "Hello World";
int vowelCount = 0;
String vowels = "aeiouAEIOU";

for (int i = 0; i < str.length(); i++) {
    if (vowels.indexOf(str.charAt(i)) != -1) {
        vowelCount++;
    }
}
System.out.println("Vowels: " + vowelCount);  // 3
```

🔹 **Word Count**
```java
String sentence = "Java is awesome";
String[] words = sentence.split(" ");
System.out.println("Word count: " + words.length);  // 3
```

---

**📝 Important Points:**
• Arrays are 0-indexed in Java
• Array size is fixed after creation
• Use `.length` for arrays, `.length()` for strings
• Strings are immutable in Java
• Use StringBuilder for multiple string operations
• Always check array bounds to avoid exceptions
• String comparison: use `.equals()`, not `==`

---

**⭐ Quick Tips for Exams:**
• Remember array declaration syntax
• Practice 2D array traversal
• Know common string methods
• Understand string immutability
• Practice string manipulation programs
• Remember difference between String and StringBuilder

---
*End of Chapter 5* ✅