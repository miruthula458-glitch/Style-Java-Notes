# 📚 JAVA NOTES - CHAPTER 9
## Collections Framework

---

### ⭐ What is Collections Framework?

**Collections Framework:** A unified architecture for representing and manipulating collections of objects

🔹 **Benefits:**
• Reduces programming effort
• Increases performance
• Provides interoperability
• Reduces effort to learn APIs
• Promotes software reuse

---

### 🔹 Collections Hierarchy

```
                    Collection (Interface)
                   /         |         \
                  /          |          \
               List       Set          Queue
            (Interface) (Interface)  (Interface)
               /  \        /  \         /  \
              /    \      /    \       /    \
        ArrayList Vector HashSet TreeSet PriorityQueue ArrayDeque
        LinkedList Stack LinkedHashSet
                         SortedSet
                           |
                         TreeSet

                    Map (Interface)
                   /         |         \
                  /          |          \
              HashMap    TreeMap    LinkedHashMap
              Hashtable  SortedMap
                           |
                         TreeMap
```

---

### ⭐ Core Interfaces

### 1. 🔹 **Collection Interface**
• Root interface of Collections Framework
• Basic operations: add, remove, size, isEmpty

### 2. 🔹 **List Interface**
• Ordered collection (sequence)
• Allows duplicate elements
• Index-based access

### 3. 🔹 **Set Interface**
• No duplicate elements
• Mathematical set abstraction

### 4. 🔹 **Queue Interface**
• FIFO (First In, First Out) ordering
• Used for holding elements before processing

### 5. 🔹 **Map Interface**
• Key-value pairs
• No duplicate keys
• Each key maps to at most one value

---

### ⭐ List Interface

### 🔹 **ArrayList**
• Resizable array implementation
• Fast random access
• Slow insertion/deletion in middle

```java
import java.util.ArrayList;

ArrayList<String> list = new ArrayList<>();

// Adding elements
list.add("Java");
list.add("Python");
list.add("C++");
list.add(1, "JavaScript");  // Insert at index 1

// Accessing elements
System.out.println(list.get(0));  // Java
System.out.println(list.size());  // 4

// Removing elements
list.remove("Python");
list.remove(0);  // Remove by index

// Iterating
for (String lang : list) {
    System.out.println(lang);
}
```

### 🔹 **LinkedList**
• Doubly-linked list implementation
• Fast insertion/deletion
• Slow random access

```java
import java.util.LinkedList;

LinkedList<Integer> list = new LinkedList<>();

// Adding elements
list.add(10);
list.add(20);
list.addFirst(5);   // Add at beginning
list.addLast(30);   // Add at end

// Accessing elements
System.out.println(list.getFirst());  // 5
System.out.println(list.getLast());   // 30

// Removing elements
list.removeFirst();
list.removeLast();
```

### 🔹 **Vector**
• Synchronized version of ArrayList
• Thread-safe but slower
• Legacy class (use ArrayList instead)

```java
import java.util.Vector;

Vector<String> vector = new Vector<>();
vector.add("Element1");
vector.add("Element2");
```

---

### ⭐ Set Interface

### 🔹 **HashSet**
• Hash table implementation
• No ordering guarantee
• Fast operations (O(1) average)

```java
import java.util.HashSet;

HashSet<String> set = new HashSet<>();

// Adding elements
set.add("Apple");
set.add("Banana");
set.add("Apple");  // Duplicate - won't be added

System.out.println(set.size());  // 2

// Checking existence
if (set.contains("Apple")) {
    System.out.println("Apple found");
}

// Iterating
for (String fruit : set) {
    System.out.println(fruit);
}
```

### 🔹 **LinkedHashSet**
• Hash table + linked list implementation
• Maintains insertion order
• Slightly slower than HashSet

```java
import java.util.LinkedHashSet;

LinkedHashSet<Integer> set = new LinkedHashSet<>();
set.add(30);
set.add(10);
set.add(20);

// Output: 30, 10, 20 (insertion order maintained)
for (Integer num : set) {
    System.out.println(num);
}
```

### 🔹 **TreeSet**
• Red-Black tree implementation
• Sorted order (natural or custom)
• Slower operations (O(log n))

```java
import java.util.TreeSet;

TreeSet<Integer> set = new TreeSet<>();
set.add(30);
set.add(10);
set.add(20);

// Output: 10, 20, 30 (sorted order)
for (Integer num : set) {
    System.out.println(num);
}

// Additional methods
System.out.println(set.first());    // 10
System.out.println(set.last());     // 30
System.out.println(set.higher(15)); // 20
```

---

### ⭐ Map Interface

### 🔹 **HashMap**
• Hash table implementation
• No ordering guarantee
• Allows one null key and multiple null values

```java
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();

// Adding key-value pairs
map.put("John", 25);
map.put("Alice", 30);
map.put("Bob", 28);

// Accessing values
System.out.println(map.get("John"));  // 25

// Checking existence
if (map.containsKey("Alice")) {
    System.out.println("Alice's age: " + map.get("Alice"));
}

// Iterating
for (String key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}

// Alternative iteration
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

### 🔹 **LinkedHashMap**
• Hash table + linked list implementation
• Maintains insertion order
• Slightly slower than HashMap

```java
import java.util.LinkedHashMap;

LinkedHashMap<String, String> map = new LinkedHashMap<>();
map.put("First", "Java");
map.put("Second", "Python");
map.put("Third", "C++");

// Output maintains insertion order
for (String key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}
```

### 🔹 **TreeMap**
• Red-Black tree implementation
• Sorted by keys (natural or custom order)
• Slower operations (O(log n))

```java
import java.util.TreeMap;

TreeMap<String, Integer> map = new TreeMap<>();
map.put("Charlie", 25);
map.put("Alice", 30);
map.put("Bob", 28);

// Output: Alice -> 30, Bob -> 28, Charlie -> 25 (sorted by keys)
for (String key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}

// Additional methods
System.out.println(map.firstKey());    // Alice
System.out.println(map.lastKey());     // Charlie
System.out.println(map.higherKey("Bob")); // Charlie
```

---

### 📊 Collections Comparison Table

| Collection | Duplicates | Ordering | Thread-Safe | Performance |
|------------|------------|----------|-------------|-------------|
| **ArrayList** | Yes | Insertion order | No | Fast access, slow insert/delete |
| **LinkedList** | Yes | Insertion order | No | Slow access, fast insert/delete |
| **Vector** | Yes | Insertion order | Yes | Slower than ArrayList |
| **HashSet** | No | No guarantee | No | Fast operations |
| **LinkedHashSet** | No | Insertion order | No | Slightly slower than HashSet |
| **TreeSet** | No | Sorted order | No | O(log n) operations |
| **HashMap** | Values: Yes, Keys: No | No guarantee | No | Fast operations |
| **LinkedHashMap** | Values: Yes, Keys: No | Insertion order | No | Slightly slower than HashMap |
| **TreeMap** | Values: Yes, Keys: No | Sorted by keys | No | O(log n) operations |

---

### ⭐ Queue Interface

### 🔹 **PriorityQueue**
• Heap-based priority queue
• Elements ordered by priority
• Not thread-safe

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();

// Adding elements
pq.offer(30);
pq.offer(10);
pq.offer(20);

// Removing elements (in priority order)
while (!pq.isEmpty()) {
    System.out.println(pq.poll());  // 10, 20, 30
}
```

### 🔹 **ArrayDeque**
• Resizable array implementation of Deque
• Can be used as stack or queue
• Faster than Stack and LinkedList

```java
import java.util.ArrayDeque;

ArrayDeque<String> deque = new ArrayDeque<>();

// Queue operations
deque.offer("First");
deque.offer("Second");
System.out.println(deque.poll());  // First

// Stack operations
deque.push("Top");
deque.push("Middle");
System.out.println(deque.pop());   // Middle
```

---

### 🔹 Iterators

### **Iterator Interface**
```java
import java.util.*;

ArrayList<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

// Using Iterator
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String element = it.next();
    System.out.println(element);
    // it.remove(); // Safe removal during iteration
}
```

### **ListIterator Interface**
```java
LinkedList<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
list.add(3);

// Bidirectional iteration
ListIterator<Integer> lit = list.listIterator();

// Forward iteration
while (lit.hasNext()) {
    System.out.println(lit.next());
}

// Backward iteration
while (lit.hasPrevious()) {
    System.out.println(lit.previous());
}
```

---

### ⭐ Collections Utility Class

**Common Methods:**
```java
import java.util.*;

List<Integer> list = Arrays.asList(3, 1, 4, 1, 5, 9);

// Sorting
Collections.sort(list);
System.out.println(list);  // [1, 1, 3, 4, 5, 9]

// Reverse
Collections.reverse(list);
System.out.println(list);  // [9, 5, 4, 3, 1, 1]

// Shuffle
Collections.shuffle(list);
System.out.println(list);  // Random order

// Binary search (list must be sorted)
Collections.sort(list);
int index = Collections.binarySearch(list, 4);
System.out.println("Index of 4: " + index);

// Min and Max
System.out.println("Min: " + Collections.min(list));
System.out.println("Max: " + Collections.max(list));

// Frequency
System.out.println("Frequency of 1: " + Collections.frequency(list, 1));

// Fill
Collections.fill(list, 0);  // Fill all elements with 0
```

---

### 🔹 Generics in Collections

**Without Generics (Raw Types):**
```java
ArrayList list = new ArrayList();
list.add("String");
list.add(123);  // Different types allowed
String str = (String) list.get(0);  // Explicit casting required
```

**With Generics:**
```java
ArrayList<String> list = new ArrayList<String>();
// ArrayList<String> list = new ArrayList<>();  // Diamond operator (Java 7+)
list.add("String");
// list.add(123);  // Compile-time error
String str = list.get(0);  // No casting required
```

---

### ⭐ Real-World Examples

### **Example 1: Student Management System**
```java
import java.util.*;

class Student {
    String name;
    int rollNo;
    double marks;
    
    Student(String name, int rollNo, double marks) {
        this.name = name;
        this.rollNo = rollNo;
        this.marks = marks;
    }
    
    @Override
    public String toString() {
        return name + " (" + rollNo + ") - " + marks;
    }
}

public class StudentManager {
    public static void main(String[] args) {
        // List to store students
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 101, 85.5));
        students.add(new Student("Bob", 102, 78.0));
        students.add(new Student("Charlie", 103, 92.5));
        
        // Map for quick lookup by roll number
        Map<Integer, Student> studentMap = new HashMap<>();
        for (Student s : students) {
            studentMap.put(s.rollNo, s);
        }
        
        // Find student by roll number
        Student found = studentMap.get(102);
        System.out.println("Found: " + found);
        
        // Sort students by marks
        Collections.sort(students, (s1, s2) -> 
            Double.compare(s2.marks, s1.marks));  // Descending order
        
        System.out.println("Top performers:");
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

### **Example 2: Word Frequency Counter**
```java
import java.util.*;

public class WordFrequency {
    public static void main(String[] args) {
        String text = "java is great java is powerful java is popular";
        String[] words = text.split(" ");
        
        // Count word frequencies
        Map<String, Integer> wordCount = new HashMap<>();
        for (String word : words) {
            wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
        }
        
        // Display results
        for (Map.Entry<String, Integer> entry : wordCount.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        
        // Find most frequent word
        String mostFrequent = Collections.max(wordCount.entrySet(),
            Map.Entry.comparingByValue()).getKey();
        System.out.println("Most frequent word: " + mostFrequent);
    }
}
```

---

### 📊 When to Use Which Collection?

```
Use ArrayList when:
• Need fast random access
• More reads than writes
• Don't need thread safety

Use LinkedList when:
• Frequent insertions/deletions
• Don't need random access
• Implementing stack/queue

Use HashSet when:
• Need unique elements
• Don't care about order
• Need fast operations

Use TreeSet when:
• Need unique elements
• Need sorted order
• Can accept slower operations

Use HashMap when:
• Need key-value mapping
• Don't care about order
• Need fast operations

Use TreeMap when:
• Need key-value mapping
• Need sorted keys
• Can accept slower operations
```

---

**📝 Important Points:**
• Collections store only objects, not primitives
• Use wrapper classes for primitives (Integer, Double, etc.)
• Always use generics for type safety
• Choose appropriate collection based on use case
• Collections are not thread-safe (except Vector, Hashtable)
• Use Collections utility class for common operations

---

**⭐ Quick Tips for Exams:**
• Remember collection hierarchy
• Know time complexities of operations
• Practice iteration methods
• Understand when to use which collection
• Know difference between Collection and Collections
• Practice real-world examples
• Remember thread-safety aspects

---
*End of Chapter 9* ✅