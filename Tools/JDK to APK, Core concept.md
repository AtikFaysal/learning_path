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
### Step1: JAVA Compiler(javac) converts .java to .class
> A **compiler** is a specialized program that translates high-level source code (like Java, C++, or Python) written by developers into low-level machine code or intermediate code that a computer’s processor can execute. The process involves multiple stages, each transforming the code incrementally to ensure correctness and optimization. Below, I’ll explain the compiler’s workflow in detail, using the provided Java code as an example, and include a conceptual diagram.

* In java, the compiler(`javac`) translate `.java` to `.class` file (`bytecode`)
* In kotlin, the compiler(`kotlinc`) translate `.kt` to `.class` file (`bytecode`)
* In C/C++, it compiles `.c/.cpp` files to `.exe` or native binaries

**How does compiler works**
*  **Lexical Analysis(Tokenizer)** 
	* Convert source code into tokens 
	* Removes whitespaces and comments
	* Detects keywords, operators, identifiers 
	* Uses a finite automaton or regular expressions to identify tokens
	* `Lexer` tools is used here 
*  **Syntax Analysis (Parser)**
	* Verifies the code syntax 
	* Converts tokens into a parser tree or *Abstract Syntax tree*(`AST`)
	* Detect syntax error like missing semicolons or incorrect statement structures are detected
*  **Semantic Analysis**
	* Type checking`(e.g., assigning an integer to a string variable)`, variables declarations 
	* Ensures logical consistency 
	* Function arguments matching 
*  **Intermediate Code Generation**
	* Convert `AST` *Abstract Syntax Tree* to intermediate code generation
	* This intermediate representation is platform independent 
*  **Optimization**
	* Improves the intermediate code to make it faster and smaller 
	* Can be at various levels: code-level, loop-level etc 
*  **Code Generation**
	* Translate optimized IR(`Intermediate Representation`) into target machine readable code or bytecode 
	* Depends on the target platform(`x86, ARM, JVM, etc`)
* **Code Linking & Assembly**
	* Combines the generated code with libraries and other object files to produce an executable
	* Produces the final executable 

![[ChatGPT Image Apr 20, 2025, 11_18_31 AM.png]]
### Step2: JAVA Runtime Environment(JRE)
> The **JAVA Runtime Environment** is a software layer that provides necessary components to run JAVA applications. It servers as the runtime environment for executing JAVA bytecode, enabling platform-independent executions of JAVA program. The `JRE` includes the **JAVA Virtual Machine(JVM)**, core JAVA class libraries, and supporting files, but it does not include development tools like compiles(`javac`), which is a part of the **JAVA Development Kit(JDK)** 

**Components of JRE**

* **JAVA Virtual Machine(JVM)**
	* `JVM` is the core engine of `JRE`, responsible for executing JAVA bytcode. It provides a platform-independent runtime environment by translating bytecode into machine-specified instructions. 
* Core JAVA Class Libraries
	* These are precompiled JAVA classes that provide essential functionality. 
	* Located in the JRE's `lib` directory
	* Provides classes like `System` and `PrintStream` from the JRE's `lib` directory. 
* Supporting Files
	* Configuring files, security policies, and native libraries(e.g. `.dll` or `.so` files) that support JVM operations and native method calls.
* JAVA Runtime Tools
	* The JAVA command-line tool, which launches the `JVM` to run JAVA program.
	* Support `JVM` operations and native method calls

![[jre.png]]

**How JRE Executes a Java Program — Step-by-Step**
User runs a Java program:
```
java HelloWorld
```
1. **JVM** is launched (inside `JRE`).
2. **Class Loader** loads `HelloWorld.class`.
3. **Bytecode Verifier** checks the class for security violations.
4. **JVM Execution Engine**:
    - **Interpreter** starts executing bytecode line by line.
    - **JIT Compiler** kicks in to compile hot paths into native machine code for better performance.
5. **Core libraries** (e.g., `System.out.println`) are called from the Java Class Library.
6. Program runs and gives output.

### Step3: JVM JAVA Virtual Machine
The **Java Virtual Machine (JVM)** is the core component of the Java Runtime Environment(`JRE`) responsible for executing Java bytecode, making Java programs platform-independent. It acts as an abstract machine that translates bytecode (produced by the `javac` compiler) into native machine code specific to the underlying hardware and operating system. The JVM also manages memory, enforces security, and optimizes performance during execution.

**Components of JVM**
* Class Loader Subsystem: Loads .class files into memory 
* Bytecode Verifier: Checks for security violations or invalid bytecode  
* Execution Engine: Execute bytecode using interpreter/JIT compiler
* Garbage Collector: Frees memory occupied by unreachable objects 
* Runtime Memory: Allocates memory to objects and method calls 
* Security Manager: Enforces security policies, restricting access to system sources 

**How JVM Works**
1. Invoking the `JVM`
	* The `JVM` allocates memory for its runtime data areas(`Heap, Method area etc`)
	* It sets up the initial thread to execute the program 
2. Class Loading
	* The `Bootstrap Class Loader` loads core Java class(e.g. `java.lang.System`, `java.io.PrintStream`) from the JRE's `lib` directory 
	* The Application Class Loader loads `.class` from current directory or class path
3. Bytecode verifier
	* The Bytecode Verifier checks `.class` file 
	* Valid bytecode instructions 
	* Type safety(e.g. `println` is called on a `PrintStream` object)
	* No illegal memory access
4. Execution Engine 
	* The Execution Engine executes the bytecode in the `main` method 
	* Interpreter translate each bytecode instruction into native machine code one at a time
	* `JIT` monitors execution to identify `hot` code(e.g frequently called methods or loops)
	* `JIT` compiles hot bytecode into native machine code for direct execution 
5. Memory Management
	* `Garbage Collector` manage memory during and after execution 
	* The `Garbage Collector` identifies and frees unreferenced objects in the Heap(e.g. temporary objects created during `println`)
	* Algorithms(e.g. mark-and-sweep) ensures efficient memory reclamation 
6. Program Termination 
	 * After `main` return `JVM` shutdown 
	 * The `Garbage Collector` frees remaining objects in the `Heap`.
	 - The JVM releases resources (e.g., threads, file handles).
	 - The `Security Manage`r ensures no unauthorized actions occur during shutdown.

![[ChatGPT Image Apr 21, 2025, 11_51_16 PM.png]]

### Step4: Interpreter
### Step5: JIT 

### Differences 

### Behind the scene of generate apk file 

