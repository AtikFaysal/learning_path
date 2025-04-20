### What is JDK:
> **JDK (Java Development Kit)** is a software development environment used for building, debugging, and running Java applications. It provides all the essential tools, libraries, and packages required to write, compile, and execute Java code. Think of it as a complete toolbox that enables developers to create robust Java applications.

**The JDK includes a wide range of tools such as:**
- **Java Runtime Environment (JRE):** Enables Java programs to run by providing the necessary runtime libraries.
- **Java Virtual Machine (JVM):** Executes compiled Java bytecode and manages system resources.
- **Java Compiler (`javac`):** Converts high-level Java code into bytecode (.class files).
- **Just-In-Time Compiler (JIT):** Optimizes bytecode during runtime for faster execution.
- **Debugger (`jdb`):** Assists in finding and fixing bugs in Java applications.
- **Java Documentation Tool (`javadoc`):** Generates documentation from code comments.
- **Java Standard Libraries:** Includes essential packages such as `java.util`, `java.io`, `java.lang`, etc.
- **Java Launcher (`java`):** Starts and runs compiled Java programs.

### How does JDK work

```
class HelloWorld{
    public static void main (String[] args) {
        System.out.println("Hello World!");
    }
}
```

Once a developer writes Java code, the JDK handles it step by step—from compilation to execution.

![[0_7JfOXNTEwCSpKlJc.png]]
### Step1: JAVA compiler(javac) converts .java to .class
> A compiler is a program that translate high-level language(java, kotlin, c++) into machine code or bytecode that can be understand by a computer or virtual machine. 

* In java, the compiler(`javac`) translate `.java` to `.class` file (`bytecode`)
* In kotlin, the compiler(`kotlinc`) translate `.kt` to `.class` file (`bytecode`)
* In C/C++, it compiles `.c/.cpp` files to `.exe` or native binaries

**How does compiler works**
1. **Lexical Analysis(Tokenizer)**
2. **Syntax Analysis (Parser)**
3. **Semantic Analysis**
4. **Intermediate Code Generation**
5. **Optimization**
6. **Code Generation**
7. **Code Linking & Assembly**

