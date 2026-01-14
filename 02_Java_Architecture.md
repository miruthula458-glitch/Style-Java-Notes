# 📚 JAVA NOTES - CHAPTER 2
## Java Architecture

---

### ⭐ JDK, JRE, JVM

🔹 **JVM (Java Virtual Machine)**
• Runtime environment for Java bytecode
• Platform-specific (Windows, Linux, Mac)
• Converts bytecode to machine code
• Provides memory management

🔹 **JRE (Java Runtime Environment)**
• JVM + Library classes + Other files
• Needed to **run** Java programs
• Contains standard Java libraries
• No development tools included

🔹 **JDK (Java Development Kit)**
• JRE + Development tools
• Needed to **develop** Java programs
• Includes compiler (javac), debugger, etc.
• Complete development environment

---

### 📊 Java Architecture Diagram

```
┌─────────────────────────────────────────┐
│                  JDK                    │
│  ┌───────────────────────────────────┐  │
│  │              JRE                  │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │           JVM               │  │  │
│  │  │  ┌─────────────────────┐    │  │  │
│  │  │  │   Class Loader      │    │  │  │
│  │  │  └─────────────────────┘    │  │  │
│  │  │  ┌─────────────────────┐    │  │  │
│  │  │  │   Bytecode Verifier │    │  │  │
│  │  │  └─────────────────────┘    │  │  │
│  │  │  ┌─────────────────────┐    │  │  │
│  │  │  │   Interpreter       │    │  │  │
│  │  │  └─────────────────────┘    │  │  │
│  │  └─────────────────────────────┘  │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │      Library Classes        │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
│  ┌───────────────────────────────────┐  │
│  │      Development Tools            │  │
│  │  • javac (compiler)              │  │
│  │  • java (interpreter)            │  │
│  │  • javadoc (documentation)       │  │
│  │  • jar (archiver)                │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

---

### 🔹 Java Program Execution Process

```
Source Code (.java)
        ↓
    [javac compiler]
        ↓
    Bytecode (.class)
        ↓
    [JVM Interpreter]
        ↓
    Machine Code
        ↓
    Output
```

**Step-by-Step Process:**

➤ **Step 1:** Write Java source code (.java file)
➤ **Step 2:** Compile using javac compiler
➤ **Step 3:** Generates bytecode (.class file)
➤ **Step 4:** JVM loads and executes bytecode
➤ **Step 5:** JIT compiler optimizes frequently used code
➤ **Step 6:** Machine code executed by OS

---

### ⭐ JVM Architecture Components

🔹 **Class Loader**
• Loads .class files into memory
• Bootstrap, Extension, Application loaders
• Dynamic loading of classes

🔹 **Memory Areas**
• **Method Area:** Stores class-level data
• **Heap:** Objects and instance variables
• **Stack:** Method calls and local variables
• **PC Register:** Current executing instruction
• **Native Method Stack:** Native method calls

🔹 **Execution Engine**
• **Interpreter:** Executes bytecode line by line
• **JIT Compiler:** Compiles frequently used code
• **Garbage Collector:** Removes unused objects

---

### 📊 Memory Management Diagram

```
┌─────────────────────────────────────┐
│            JVM Memory               │
├─────────────────────────────────────┤
│  Method Area (Metaspace)            │
│  • Class metadata                   │
│  • Constant pool                    │
│  • Static variables                 │
├─────────────────────────────────────┤
│  Heap Memory                        │
│  ┌─────────────┬─────────────────┐  │
│  │ Young Gen   │   Old Gen       │  │
│  │ • Eden      │   • Tenured     │  │
│  │ • Survivor  │     Space       │  │
│  └─────────────┴─────────────────┘  │
├─────────────────────────────────────┤
│  Stack Memory                       │
│  • Method calls                     │
│  • Local variables                  │
│  • Partial results                  │
├─────────────────────────────────────┤
│  PC (Program Counter) Register      │
│  • Current instruction address      │
├─────────────────────────────────────┤
│  Native Method Stack                │
│  • Native method calls              │
└─────────────────────────────────────┘
```

---

### 🔹 Platform Independence

**How Java achieves Platform Independence:**

```
Windows Machine          Linux Machine          Mac Machine
      ↓                        ↓                     ↓
  Windows JVM              Linux JVM             Mac JVM
      ↓                        ↓                     ↓
      └────────── Same Bytecode (.class) ──────────┘
```

➤ Java source code compiled to bytecode
➤ Bytecode is platform-neutral
➤ Each OS has its own JVM
➤ JVM translates bytecode to native machine code

---

### ⭐ Key Points to Remember

• **JVM** is platform-specific
• **Bytecode** is platform-independent
• **JRE** = JVM + Libraries
• **JDK** = JRE + Development Tools
• Java follows **"Compile once, run anywhere"**
• **Garbage Collection** is automatic in Java
• **JIT Compiler** improves performance

---

**📝 Commands to Remember:**
• `javac filename.java` - Compile Java file
• `java classname` - Run Java program
• `java -version` - Check Java version
• `javac -version` - Check compiler version

---
*End of Chapter 2* ✅