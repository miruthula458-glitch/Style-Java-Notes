# 📚 JAVA NOTES - CHAPTER 11
## File Handling

---

### ⭐ What is File Handling?

**File Handling:** Process of creating, reading, writing, and manipulating files using Java programs

🔹 **Why File Handling?**
• Store data permanently
• Read configuration files
• Process large datasets
• Create logs and reports
• Data backup and recovery

---

### 🔹 File Class

**File Class:** Represents files and directories in the file system

```java
import java.io.File;

// Creating File objects
File file1 = new File("data.txt");                    // Current directory
File file2 = new File("C:\\Users\\Documents\\data.txt"); // Absolute path
File file3 = new File("folder", "data.txt");          // Directory + filename
```

### **Important File Methods:**

| Method | Description | Example |
|--------|-------------|---------|
| `exists()` | Check if file exists | `file.exists()` |
| `createNewFile()` | Create new file | `file.createNewFile()` |
| `delete()` | Delete file | `file.delete()` |
| `getName()` | Get file name | `file.getName()` |
| `getPath()` | Get file path | `file.getPath()` |
| `getAbsolutePath()` | Get absolute path | `file.getAbsolutePath()` |
| `length()` | Get file size in bytes | `file.length()` |
| `isFile()` | Check if it's a file | `file.isFile()` |
| `isDirectory()` | Check if it's a directory | `file.isDirectory()` |
| `canRead()` | Check if readable | `file.canRead()` |
| `canWrite()` | Check if writable | `file.canWrite()` |
| `mkdir()` | Create directory | `file.mkdir()` |
| `mkdirs()` | Create directory tree | `file.mkdirs()` |
| `list()` | List files in directory | `file.list()` |
| `listFiles()` | Get File objects array | `file.listFiles()` |

---

### ⭐ File Operations Example

```java
import java.io.File;
import java.io.IOException;

public class FileOperationsExample {
    public static void main(String[] args) {
        try {
            // Create File object
            File file = new File("example.txt");
            
            // Check if file exists
            if (file.exists()) {
                System.out.println("File already exists");
            } else {
                // Create new file
                if (file.createNewFile()) {
                    System.out.println("File created: " + file.getName());
                }
            }
            
            // File information
            System.out.println("File name: " + file.getName());
            System.out.println("Absolute path: " + file.getAbsolutePath());
            System.out.println("File size: " + file.length() + " bytes");
            System.out.println("Can read: " + file.canRead());
            System.out.println("Can write: " + file.canWrite());
            System.out.println("Is file: " + file.isFile());
            System.out.println("Is directory: " + file.isDirectory());
            
            // Create directory
            File dir = new File("testFolder");
            if (dir.mkdir()) {
                System.out.println("Directory created: " + dir.getName());
            }
            
            // List files in current directory
            File currentDir = new File(".");
            String[] files = currentDir.list();
            System.out.println("\nFiles in current directory:");
            for (String fileName : files) {
                System.out.println(fileName);
            }
            
        } catch (IOException e) {
            System.out.println("An error occurred: " + e.getMessage());
        }
    }
}
```

---

### ⭐ Java I/O Streams

**Stream:** Sequence of data flowing from source to destination

### 📊 Stream Hierarchy

```
                    Stream
                   /      \
            InputStream   OutputStream
           /     |    \    /    |    \
    FileInput ByteArray Filter FileOutput ByteArray Filter
    Stream    Input    Input   Stream     Output    Output
              Stream   Stream             Stream    Stream
                |                           |
         BufferedInput                BufferedOutput
         Stream                       Stream

                Character Streams
                   /        \
                Reader     Writer
               /    \      /    \
        FileReader Buffer FileWriter Buffer
                   Reader          Writer
```

---

### 🔹 Types of Streams

### **1. Byte Streams**
• Handle binary data (images, videos, etc.)
• Base classes: `InputStream` and `OutputStream`

### **2. Character Streams**
• Handle text data
• Base classes: `Reader` and `Writer`

---

### ⭐ Reading Files

### 🔹 Method 1: FileInputStream (Byte Stream)

```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileReadExample1 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("data.txt");
            int data;
            
            // Read byte by byte
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        } finally {
            try {
                if (fis != null) {
                    fis.close();
                }
            } catch (IOException e) {
                System.out.println("Error closing file: " + e.getMessage());
            }
        }
    }
}
```

### 🔹 Method 2: FileReader (Character Stream)

```java
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample2 {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("data.txt")) {
            int character;
            
            // Read character by character
            while ((character = fr.read()) != -1) {
                System.out.print((char) character);
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```

### 🔹 Method 3: BufferedReader (Efficient Reading)

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileReadExample3 {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
            String line;
            
            // Read line by line
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```

### 🔹 Method 4: Scanner Class

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class FileReadExample4 {
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(new File("data.txt"))) {
            
            // Read line by line
            while (scanner.hasNextLine()) {
                String line = scanner.nextLine();
                System.out.println(line);
            }
            
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```

---

### ⭐ Writing Files

### 🔹 Method 1: FileOutputStream (Byte Stream)

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileWriteExample1 {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            String data = "Hello, World!\nThis is file writing example.";
            byte[] bytes = data.getBytes();
            
            fos.write(bytes);
            System.out.println("Data written to file successfully");
            
        } catch (IOException e) {
            System.out.println("Error writing to file: " + e.getMessage());
        }
    }
}
```

### 🔹 Method 2: FileWriter (Character Stream)

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriteExample2 {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("output.txt")) {
            fw.write("Hello, World!\n");
            fw.write("This is written using FileWriter.\n");
            fw.write("Java file handling is easy!");
            
            System.out.println("Data written successfully");
            
        } catch (IOException e) {
            System.out.println("Error writing to file: " + e.getMessage());
        }
    }
}
```

### 🔹 Method 3: BufferedWriter (Efficient Writing)

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class FileWriteExample3 {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            bw.write("Line 1: Hello World");
            bw.newLine();  // Add new line
            bw.write("Line 2: Java Programming");
            bw.newLine();
            bw.write("Line 3: File Handling");
            
            System.out.println("Data written using BufferedWriter");
            
        } catch (IOException e) {
            System.out.println("Error writing to file: " + e.getMessage());
        }
    }
}
```

### 🔹 Method 4: PrintWriter

```java
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

public class FileWriteExample4 {
    public static void main(String[] args) {
        try (PrintWriter pw = new PrintWriter(new FileWriter("output.txt"))) {
            pw.println("Hello World");
            pw.println("Number: " + 42);
            pw.printf("Formatted: %.2f%n", 3.14159);
            
            System.out.println("Data written using PrintWriter");
            
        } catch (IOException e) {
            System.out.println("Error writing to file: " + e.getMessage());
        }
    }
}
```

---

### 🔹 Append to File

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileAppendExample {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("data.txt", true)) {  // true for append mode
            fw.write("\nThis line is appended to existing file.");
            fw.write("\nAnother appended line.");
            
            System.out.println("Data appended successfully");
            
        } catch (IOException e) {
            System.out.println("Error appending to file: " + e.getMessage());
        }
    }
}
```

---

### ⭐ File Copy Example

```java
import java.io.*;

public class FileCopyExample {
    public static void main(String[] args) {
        String sourceFile = "source.txt";
        String destinationFile = "destination.txt";
        
        try (FileInputStream fis = new FileInputStream(sourceFile);
             FileOutputStream fos = new FileOutputStream(destinationFile)) {
            
            byte[] buffer = new byte[1024];
            int bytesRead;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);
            }
            
            System.out.println("File copied successfully");
            
        } catch (IOException e) {
            System.out.println("Error copying file: " + e.getMessage());
        }
    }
}
```

---

### 🔹 Reading Different Data Types

```java
import java.io.*;

public class DataTypesFileExample {
    public static void main(String[] args) {
        // Writing different data types
        try (DataOutputStream dos = new DataOutputStream(
                new FileOutputStream("data.dat"))) {
            
            dos.writeInt(123);
            dos.writeDouble(45.67);
            dos.writeBoolean(true);
            dos.writeUTF("Hello World");
            
            System.out.println("Data written successfully");
            
        } catch (IOException e) {
            System.out.println("Error writing data: " + e.getMessage());
        }
        
        // Reading different data types
        try (DataInputStream dis = new DataInputStream(
                new FileInputStream("data.dat"))) {
            
            int intValue = dis.readInt();
            double doubleValue = dis.readDouble();
            boolean boolValue = dis.readBoolean();
            String stringValue = dis.readUTF();
            
            System.out.println("Integer: " + intValue);
            System.out.println("Double: " + doubleValue);
            System.out.println("Boolean: " + boolValue);
            System.out.println("String: " + stringValue);
            
        } catch (IOException e) {
            System.out.println("Error reading data: " + e.getMessage());
        }
    }
}
```

---

### ⭐ Serialization

**Serialization:** Converting object into byte stream for storage or transmission

```java
import java.io.*;

// Serializable class
class Student implements Serializable {
    private static final long serialVersionUID = 1L;
    
    String name;
    int age;
    transient String password;  // transient fields are not serialized
    
    public Student(String name, int age, String password) {
        this.name = name;
        this.age = age;
        this.password = password;
    }
    
    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + ", password='" + password + "'}";
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Student student = new Student("John", 20, "secret123");
        
        // Serialization (Writing object to file)
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream("student.ser"))) {
            
            oos.writeObject(student);
            System.out.println("Object serialized successfully");
            
        } catch (IOException e) {
            System.out.println("Error during serialization: " + e.getMessage());
        }
        
        // Deserialization (Reading object from file)
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream("student.ser"))) {
            
            Student deserializedStudent = (Student) ois.readObject();
            System.out.println("Object deserialized: " + deserializedStudent);
            
        } catch (IOException | ClassNotFoundException e) {
            System.out.println("Error during deserialization: " + e.getMessage());
        }
    }
}
```

---

### 📊 File Handling Best Practices

```
File Handling Best Practices:

1. Always use try-with-resources
   ├── Automatic resource management
   └── Ensures proper closing

2. Handle exceptions properly
   ├── IOException for file operations
   ├── FileNotFoundException for missing files
   └── SecurityException for access issues

3. Use appropriate stream types
   ├── Byte streams for binary data
   ├── Character streams for text data
   └── Buffered streams for efficiency

4. Check file existence before operations
   ├── file.exists()
   ├── file.canRead()
   └── file.canWrite()

5. Use absolute paths when necessary
   ├── Avoid relative path issues
   └── Better for production applications
```

---

### ⭐ Real-World Example: Log File Manager

```java
import java.io.*;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class LogFileManager {
    private String logFileName;
    private DateTimeFormatter formatter;
    
    public LogFileManager(String logFileName) {
        this.logFileName = logFileName;
        this.formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
    }
    
    public void writeLog(String level, String message) {
        try (PrintWriter pw = new PrintWriter(new FileWriter(logFileName, true))) {
            String timestamp = LocalDateTime.now().format(formatter);
            pw.println("[" + timestamp + "] [" + level + "] " + message);
        } catch (IOException e) {
            System.err.println("Error writing to log file: " + e.getMessage());
        }
    }
    
    public void readLogs() {
        try (BufferedReader br = new BufferedReader(new FileReader(logFileName))) {
            String line;
            System.out.println("=== Log File Contents ===");
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error reading log file: " + e.getMessage());
        }
    }
    
    public void clearLogs() {
        try (PrintWriter pw = new PrintWriter(new FileWriter(logFileName))) {
            // Opening in write mode clears the file
            System.out.println("Log file cleared successfully");
        } catch (IOException e) {
            System.err.println("Error clearing log file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        LogFileManager logger = new LogFileManager("application.log");
        
        // Write some logs
        logger.writeLog("INFO", "Application started");
        logger.writeLog("DEBUG", "Processing user request");
        logger.writeLog("ERROR", "Database connection failed");
        logger.writeLog("INFO", "Application stopped");
        
        // Read logs
        logger.readLogs();
    }
}
```

---

### 🔹 File Processing Example: CSV Reader

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class CSVReader {
    public static void main(String[] args) {
        String csvFile = "students.csv";
        String line;
        String csvSplitBy = ",";
        
        try (BufferedReader br = new BufferedReader(new FileReader(csvFile))) {
            // Read header
            String header = br.readLine();
            System.out.println("Header: " + header);
            System.out.println("------------------------");
            
            // Read data rows
            while ((line = br.readLine()) != null) {
                String[] data = line.split(csvSplitBy);
                
                if (data.length >= 3) {
                    String name = data[0].trim();
                    String age = data[1].trim();
                    String grade = data[2].trim();
                    
                    System.out.println("Name: " + name + 
                                     ", Age: " + age + 
                                     ", Grade: " + grade);
                }
            }
            
        } catch (IOException e) {
            System.out.println("Error reading CSV file: " + e.getMessage());
        }
    }
}
```

---

**📝 Important Points:**
• Always close streams to prevent resource leaks
• Use try-with-resources for automatic resource management
• Choose appropriate stream type based on data
• Handle exceptions properly
• Use buffered streams for better performance
• Check file permissions before operations
• Use absolute paths in production applications
• Consider thread safety for concurrent file access

---

**⭐ Quick Tips for Exams:**
• Remember stream hierarchy
• Know difference between byte and character streams
• Practice file operations (create, read, write, delete)
• Understand serialization concepts
• Know when to use buffered streams
• Practice exception handling in file operations
• Remember try-with-resources syntax
• Practice real-world file processing examples

---
*End of Chapter 11* ✅