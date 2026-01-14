# JAVA NOTES - CHAPTER 12
## Java Input/Output (I/O)

---

### What is Java I/O?

**Java I/O:** Package that provides classes and interfaces for system input and output through data streams, serialization, and file system

 **Key Concepts:**
• **Stream:** Sequence of data
• **Input Stream:** Reading data from source
• **Output Stream:** Writing data to destination
• **Buffer:** Temporary storage for efficient I/O

---

### Java I/O Class Hierarchy

```
                    Object
                      │
              ┌───────┴───────┐
              │               │
         InputStream      OutputStream
         /    |    \      /    |    \
    FileInput ByteArray Filter FileOutput ByteArray Filter
    Stream    Input    Input   Stream     Output    Output
              Stream   Stream             Stream    Stream
                │                           │
         BufferedInput                BufferedOutput
         Stream                       Stream
              │                           │
        DataInput                   DataOutput
        Stream                      Stream
              │                           │
        ObjectInput                 ObjectOutput
        Stream                      Stream

                Character I/O
                      │
              ┌───────┴───────┐
              │               │
            Reader          Writer
           /   |   \        /   |   \
    FileReader Input Buffer FileWriter Output Buffer
               Reader Reader          Writer Writer
                 │                      │
           BufferedReader        BufferedWriter
                 │                      │
           LineNumberReader      PrintWriter
```

---

### Types of Streams

### **1.Byte Streams**
• Handle 8-bit bytes
• Used for binary data (images, videos, executables)
• Base classes: `InputStream` and `OutputStream`

### **2.Character Streams**
• Handle 16-bit Unicode characters
• Used for text data
• Base classes: `Reader` and `Writer`

---

### Byte Streams

### **InputStream (Abstract Class)**

**Common Methods:**
```java
int read()                    // Read single byte
int read(byte[] b)           // Read into byte array
int read(byte[] b, int off, int len)  // Read with offset and length
void close()                 // Close stream
int available()              // Available bytes to read
long skip(long n)            // Skip n bytes
boolean markSupported()      // Check if mark/reset supported
void mark(int readlimit)     // Mark current position
void reset()                 // Reset to marked position
```

### **FileInputStream Example**

```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStreamExample {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("input.txt")) {
            
            // Method 1: Read byte by byte
            System.out.println("Reading byte by byte:");
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: Read into byte array
        try (FileInputStream fis = new FileInputStream("input.txt")) {
            
            byte[] buffer = new byte[1024];
            int bytesRead;
            
            System.out.println("\nReading with buffer:");
            while ((bytesRead = fis.read(buffer)) != -1) {
                String content = new String(buffer, 0, bytesRead);
                System.out.print(content);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### **OutputStream (Abstract Class)**

**Common Methods:**
```java
void write(int b)                    // Write single byte
void write(byte[] b)                 // Write byte array
void write(byte[] b, int off, int len)  // Write with offset and length
void flush()                         // Force write buffered data
void close()                         // Close stream
```

### **FileOutputStream Example**

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamExample {
    public static void main(String[] args) {
        // Method 1: Write string as bytes
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            
            String data = "Hello World!\nJava I/O Streams";
            byte[] bytes = data.getBytes();
            fos.write(bytes);
            
            System.out.println("Data written successfully");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: Write byte by byte
        try (FileOutputStream fos = new FileOutputStream("output2.txt")) {
            
            String data = "Byte by byte writing";
            for (int i = 0; i < data.length(); i++) {
                fos.write(data.charAt(i));
            }
            
            System.out.println("Data written byte by byte");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### **BufferedInputStream and BufferedOutputStream**

**Benefits:**
• Reduces system calls
• Improves performance
• Internal buffer for efficient I/O

```java
import java.io.*;

public class BufferedStreamExample {
    public static void main(String[] args) {
        // Writing with BufferedOutputStream
        try (BufferedOutputStream bos = new BufferedOutputStream(
                new FileOutputStream("buffered.txt"))) {
            
            String data = "This is buffered output stream example.\n";
            data += "It improves performance by reducing system calls.\n";
            data += "Data is written to internal buffer first.";
            
            bos.write(data.getBytes());
            bos.flush();  // Force write buffer to file
            
            System.out.println("Data written using BufferedOutputStream");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Reading with BufferedInputStream
        try (BufferedInputStream bis = new BufferedInputStream(
                new FileInputStream("buffered.txt"))) {
            
            byte[] buffer = new byte[1024];
            int bytesRead;
            
            System.out.println("Reading using BufferedInputStream:");
            while ((bytesRead = bis.read(buffer)) != -1) {
                String content = new String(buffer, 0, bytesRead);
                System.out.print(content);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### **DataInputStream and DataOutputStream**

**Purpose:** Read/write primitive data types in binary format

```java
import java.io.*;

public class DataStreamExample {
    public static void main(String[] args) {
        // Writing primitive data types
        try (DataOutputStream dos = new DataOutputStream(
                new FileOutputStream("primitives.dat"))) {
            
            dos.writeInt(42);
            dos.writeDouble(3.14159);
            dos.writeBoolean(true);
            dos.writeChar('A');
            dos.writeUTF("Hello World");  // Modified UTF-8
            dos.writeLong(1234567890L);
            dos.writeFloat(2.5f);
            dos.writeShort((short) 100);
            dos.writeByte((byte) 255);
            
            System.out.println("Primitive data written successfully");
            
        } catch (IOException e) {
            System.out.println("Error writing: " + e.getMessage());
        }
        
        // Reading primitive data types
        try (DataInputStream dis = new DataInputStream(
                new FileInputStream("primitives.dat"))) {
            
            int intValue = dis.readInt();
            double doubleValue = dis.readDouble();
            boolean boolValue = dis.readBoolean();
            char charValue = dis.readChar();
            String stringValue = dis.readUTF();
            long longValue = dis.readLong();
            float floatValue = dis.readFloat();
            short shortValue = dis.readShort();
            byte byteValue = dis.readByte();
            
            System.out.println("Reading primitive data:");
            System.out.println("int: " + intValue);
            System.out.println("double: " + doubleValue);
            System.out.println("boolean: " + boolValue);
            System.out.println("char: " + charValue);
            System.out.println("String: " + stringValue);
            System.out.println("long: " + longValue);
            System.out.println("float: " + floatValue);
            System.out.println("short: " + shortValue);
            System.out.println("byte: " + byteValue);
            
        } catch (IOException e) {
            System.out.println("Error reading: " + e.getMessage());
        }
    }
}
```

---

### Character Streams

### **Reader (Abstract Class)**

**Common Methods:**
```java
int read()                           // Read single character
int read(char[] cbuf)               // Read into character array
int read(char[] cbuf, int off, int len)  // Read with offset and length
void close()                        // Close stream
boolean ready()                     // Check if ready to read
long skip(long n)                   // Skip n characters
boolean markSupported()             // Check if mark/reset supported
void mark(int readAheadLimit)       // Mark current position
void reset()                        // Reset to marked position
```

### **FileReader Example**

```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderExample {
    public static void main(String[] args) {
        // Method 1: Read character by character
        try (FileReader fr = new FileReader("text.txt")) {
            
            int character;
            System.out.println("Reading character by character:");
            while ((character = fr.read()) != -1) {
                System.out.print((char) character);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: Read into character array
        try (FileReader fr = new FileReader("text.txt")) {
            
            char[] buffer = new char[1024];
            int charsRead;
            
            System.out.println("\nReading with character buffer:");
            while ((charsRead = fr.read(buffer)) != -1) {
                String content = new String(buffer, 0, charsRead);
                System.out.print(content);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### **Writer (Abstract Class)**

**Common Methods:**
```java
void write(int c)                    // Write single character
void write(char[] cbuf)              // Write character array
void write(char[] cbuf, int off, int len)  // Write with offset and length
void write(String str)               // Write string
void write(String str, int off, int len)   // Write substring
void flush()                         // Force write buffered data
void close()                         // Close stream
```

### **FileWriter Example**

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        // Method 1: Write string
        try (FileWriter fw = new FileWriter("output.txt")) {
            
            fw.write("Hello World!\n");
            fw.write("This is FileWriter example.\n");
            fw.write("Character streams handle Unicode properly.");
            
            System.out.println("Text written using FileWriter");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Method 2: Write character array
        try (FileWriter fw = new FileWriter("output2.txt")) {
            
            char[] chars = {'J', 'a', 'v', 'a', ' ', 'I', '/', 'O'};
            fw.write(chars);
            
            System.out.println("Character array written");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### **BufferedReader and BufferedWriter**

```java
import java.io.*;

public class BufferedCharacterStreamExample {
    public static void main(String[] args) {
        // Writing with BufferedWriter
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("buffered.txt"))) {
            
            bw.write("Line 1: BufferedWriter Example");
            bw.newLine();  // Platform-independent new line
            bw.write("Line 2: Efficient character I/O");
            bw.newLine();
            bw.write("Line 3: Internal buffering improves performance");
            
            System.out.println("Text written using BufferedWriter");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Reading with BufferedReader
        try (BufferedReader br = new BufferedReader(new FileReader("buffered.txt"))) {
            
            String line;
            int lineNumber = 1;
            
            System.out.println("Reading using BufferedReader:");
            while ((line = br.readLine()) != null) {
                System.out.println(lineNumber + ": " + line);
                lineNumber++;
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### **PrintWriter**

**Features:**
• Convenient methods for formatted output
• Automatic flushing option
• Never throws IOException

```java
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

public class PrintWriterExample {
    public static void main(String[] args) {
        try (PrintWriter pw = new PrintWriter(new FileWriter("formatted.txt"))) {
            
            // Various print methods
            pw.println("Hello World");
            pw.println(42);
            pw.println(3.14159);
            pw.println(true);
            
            // Formatted output
            pw.printf("Name: %s, Age: %d, Salary: %.2f%n", "John", 25, 50000.75);
            pw.printf("Formatted number: %,d%n", 1234567);
            pw.printf("Percentage: %.1f%%%n", 85.5);
            
            // Print arrays
            int[] numbers = {1, 2, 3, 4, 5};
            pw.print("Array: ");
            for (int num : numbers) {
                pw.print(num + " ");
            }
            pw.println();
            
            System.out.println("Formatted output written successfully");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### Standard I/O Streams

### **System.in, System.out, System.err**

```java
import java.io.*;

public class StandardIOExample {
    public static void main(String[] args) {
        // System.out - Standard output
        System.out.println("This goes to standard output");
        
        // System.err - Standard error
        System.err.println("This goes to standard error");
        
        // System.in - Standard input
        try (BufferedReader br = new BufferedReader(
                new InputStreamReader(System.in))) {
            
            System.out.print("Enter your name: ");
            String name = br.readLine();
            
            System.out.print("Enter your age: ");
            String ageStr = br.readLine();
            int age = Integer.parseInt(ageStr);
            
            System.out.println("Hello " + name + ", you are " + age + " years old.");
            
        } catch (IOException e) {
            System.err.println("Error reading input: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Invalid age format: " + e.getMessage());
        }
    }
}
```

---

### **Console Class**

```java
import java.io.Console;

public class ConsoleExample {
    public static void main(String[] args) {
        Console console = System.console();
        
        if (console == null) {
            System.out.println("Console not available");
            return;
        }
        
        // Read line
        String name = console.readLine("Enter your name: ");
        
        // Read password (characters not echoed)
        char[] password = console.readPassword("Enter password: ");
        
        console.printf("Hello %s!%n", name);
        console.printf("Password length: %d%n", password.length);
        
        // Clear password from memory
        java.util.Arrays.fill(password, ' ');
    }
}
```

---

### Stream Conversion

### **InputStreamReader and OutputStreamWriter**

```java
import java.io.*;
import java.nio.charset.StandardCharsets;

public class StreamConversionExample {
    public static void main(String[] args) {
        // Convert byte stream to character stream
        try (InputStreamReader isr = new InputStreamReader(
                new FileInputStream("input.txt"), StandardCharsets.UTF_8);
             BufferedReader br = new BufferedReader(isr)) {
            
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
        // Convert character stream to byte stream
        try (OutputStreamWriter osw = new OutputStreamWriter(
                new FileOutputStream("output.txt"), StandardCharsets.UTF_8);
             BufferedWriter bw = new BufferedWriter(osw)) {
            
            bw.write("This text is written using OutputStreamWriter");
            bw.newLine();
            bw.write("It converts character stream to byte stream");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

### Stream Comparison Table

| Feature | Byte Streams | Character Streams |
|---------|--------------|-------------------|
| **Data Type** | 8-bit bytes | 16-bit characters |
| **Base Classes** | InputStream/OutputStream | Reader/Writer |
| **Use Case** | Binary data | Text data |
| **Encoding** | No automatic encoding | Handles character encoding |
| **Performance** | Faster for binary data | Better for text processing |
| **Examples** | Images, videos, executables | Text files, XML, JSON |

---

### Real-World Example: File Processor

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;

public class FileProcessor {
    
    // Method 1: Process large file line by line (memory efficient)
    public void processLargeFile(String fileName) {
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            int lineCount = 0;
            int wordCount = 0;
            
            while ((line = br.readLine()) != null) {
                lineCount++;
                wordCount += line.split("\\s+").length;
            }
            
            System.out.println("File: " + fileName);
            System.out.println("Lines: " + lineCount);
            System.out.println("Words: " + wordCount);
            
        } catch (IOException e) {
            System.out.println("Error processing file: " + e.getMessage());
        }
    }
    
    // Method 2: Read entire file into memory (for small files)
    public void readEntireFile(String fileName) {
        try {
            List<String> lines = Files.readAllLines(Paths.get(fileName));
            
            System.out.println("File contents:");
            for (int i = 0; i < lines.size(); i++) {
                System.out.println((i + 1) + ": " + lines.get(i));
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
    
    // Method 3: Copy file with progress indication
    public void copyFileWithProgress(String source, String destination) {
        try (FileInputStream fis = new FileInputStream(source);
             FileOutputStream fos = new FileOutputStream(destination)) {
            
            byte[] buffer = new byte[8192];  // 8KB buffer
            long totalBytes = new File(source).length();
            long copiedBytes = 0;
            int bytesRead;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);
                copiedBytes += bytesRead;
                
                // Show progress
                int progress = (int) ((copiedBytes * 100) / totalBytes);
                System.out.print("\rProgress: " + progress + "%");
            }
            
            System.out.println("\nFile copied successfully!");
            
        } catch (IOException e) {
            System.out.println("Error copying file: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        FileProcessor processor = new FileProcessor();
        
        // Create sample file
        try (PrintWriter pw = new PrintWriter("sample.txt")) {
            pw.println("This is line 1");
            pw.println("This is line 2 with more words");
            pw.println("Final line of the sample file");
        } catch (IOException e) {
            System.out.println("Error creating sample file");
        }
        
        // Process the file
        processor.processLargeFile("sample.txt");
        processor.readEntireFile("sample.txt");
        processor.copyFileWithProgress("sample.txt", "copy_sample.txt");
    }
}
```

---

### Performance Tips

```java
// ❌ Inefficient - No buffering
try (FileReader fr = new FileReader("large.txt")) {
    int ch;
    while ((ch = fr.read()) != -1) {
        // Process character
    }
}

// ✅ Efficient - With buffering
try (BufferedReader br = new BufferedReader(new FileReader("large.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        // Process line
    }
}

// ✅ Even more efficient - Larger buffer
try (BufferedReader br = new BufferedReader(new FileReader("large.txt"), 16384)) {
    String line;
    while ((line = br.readLine()) != null) {
        // Process line
    }
}
```

---

**Important Points:**
• Use byte streams for binary data, character streams for text
• Always use buffered streams for better performance
• Character streams handle Unicode encoding automatically
• Use try-with-resources for automatic resource management
• Choose appropriate buffer size based on file size
• DataInputStream/DataOutputStream preserve data types
• PrintWriter provides convenient formatting methods
• Console class is useful for command-line applications

---
*End of Chapter 12* ✅