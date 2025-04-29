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

**How Does JVM Work**
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
> An interpreter is a program that executes code written in a high-level programming language by translating and running it line-by-line or statement-by-statement, without requiring a separate compilation step. Unlike a compiler, which translates the entire program into machine code before execution, an interpreter processes the code dynamically, making it suitable for scripting, interactive environments, and rapid prototyping.

**Key Features of Intercepters**
* Line-by-line execution: Executes one statement at a time during runtime 
* No separate compilation: Code is not translated into machine code ahead of time 
* Slower than compiler: Because of it interprets during every run
* Better debugging: Errors are easier to trace as they're caught as the code is read
* Dynamic typing: Often used in dynamically-typed languages like python and Javascript 

**How does Interpreter work**
* **Source code input:** The interpreter receives the source code written  in high-level programing language(e.g. Java, Python, JavaScript or Ruby). This code is typically human-readable and consists of instructions like variable declarations, loops or functions calls 
* **Lexical analysis:** The interpreter's `Lexer` breaks the source code into a sequence of tokens. Tokens are the smallest meaningful units, such as keywords `if`, `while`, identifiers (`x`, `myFunction`)
* **Syntax analysis:** The parser takes the token stream and constructs the `Abstract Syntax Tree(AST)`, which represents the hierarchical structure of the code according to the language's grammar rules. The parser checks for syntax errors (e.g., missing parentheses or incorrect keywords). If the syntax is valid, the `AST` captures the program’s structure, such as expressions, statements, or blocks.
* **Semantic Analysis:** The interpreter performs semantic checks to ensure the code makes logical sense. This includes verifying variable declarations, type compatibility, and scope rules. For example, it checks if x is defined before use or if 5 + "hello" is a valid operation in the language. Some interpreters maintain a symbol table to track variables and their values or types.
* **Intermediate Representation (Optional):** Some interpreters (e.g., Python, JavaScript) convert the AST into an intermediate representation (IR), like bytecode, for efficiency. Bytecode is a low-level, platform-independent representation of the program that is easier to execute than raw `AST`. Example, Python’s interpreter compiles source code to bytecode (stored in .pyc files) before execution.
* **Execution**: - The interpreter’s execution engine processes the AST or bytecode and performs the corresponding operations. This involves:
    - **Evaluating expressions**: Computing results like 5 + 3 = 8.
    - **Managing memory**: Allocating space for variables and objects.
    - **Handling control flow**: Executing loops, conditionals, or function calls.
    - **Interacting with the runtime environment**: Accessing system resources, libraries, or I/O.
- **Output or Interaction**: The interpreter produces output (e.g., printing to the console) or updates the program’s state (e.g., modifying variables). In interactive environments like Python’s REPL, it waits for the next input. If an error occurs (e.g., runtime exception), the interpreter halts and reports it.
- **Runtime Environment**: The interpreter maintains a runtime environment, including:
	- **Stack**: For function calls and local variables.
	- **Heap**: For dynamic memory allocation (e.g., objects, arrays).
	- **Standard Library**: For built-in functions and modules.
![[ChatGPT Image Apr 23, 2025, 05_41_21 PM.png]]
### Step5: JIT 
>The **Just-In-Time (JIT) Compiler** is a critical component of the Java Virtual Machine (JVM) that dynamically compiles Java bytecode into native machine code during a program's runtime to improve performance. Unlike traditional compilers that generate machine code before execution (ahead-of-time compilation), the JIT compiler performs compilation on-the-fly, optimizing code based on runtime behavior. This allows Java programs to combine the portability of bytecode with execution speeds approaching those of natively compiled languages like C++.

**Why JIT needed**
The JIT compiler is part of the JVM’s **Execution Engine** and serves to:
- **Translate Bytecode to Native Code**: Converts platform-independent bytecode into machine-specific instructions that the underlying hardware can execute directly.
- **Optimize Performance**: Applies optimizations based on runtime data, such as frequently executed code paths (hotspots), to reduce execution time.
- **Balance Startup and Performance**: Works alongside the JVM’s interpreter to provide quick startup (via interpretation) and optimized execution (via compilation).

The JIT compiler is key to Java’s performance, enabling it to rival native applications by generating optimized machine code tailored to the specific runtime environment.

**How does JIT Compiler work?**
The JIT compiler operates dynamically during program execution, compiling bytecode into native machine code based on runtime profiling. It works in tandem with the JVM’s interpreter and uses a **hotspot** approach to focus on frequently executed code. Below is a step-by-step explanation of the process.

1. **Program Invocation**:
	- The JVM starts when you run a Java program (e.g., java HelloWorld).
	- The JVM loads the .class file, verifies its bytecode, and begins execution.
2. **Initial Execution with Interpreter**:
	- The JVM’s **Interpreter** executes bytecode by translating each instruction into native machine code one at a time.
    - This provides quick startup but is slower for repeated execution.
3. **Profiling and Hotspot Detection**:
	- The JIT compiler monitors the running program to identify **hotspots**—code segments (methods, loops) executed frequently.
	- It collects runtime data, such as:
    - How often a method is called.
    - Which code paths are taken most frequently.
    - Variable usage patterns.
	- The JVM uses counters to track method invocations and loop iterations.
4. **Compilation of Hotspots**:
	- When a method or loop exceeds a threshold (e.g., called 10,000 times), the JIT compiler compiles its bytecode into native machine code.
    - The compilation is performed at different **tiers** (in modern JVMs like HotSpot):
	    - **C1 Compiler** (Client): Fast compilation with basic optimizations for quick results.
	    - **C2 Compiler** (Server): Slower, more aggressive optimizations for maximum performance.
	    - **Tiered Compilation**: Combines C1 and C2, starting with C1 and later applying C2 for heavily used code.
5. **Optimization**:
	- The JIT compiler applies optimizations based on runtime data, including:
	    - **Inlining**: Replacing method calls with the method’s body to reduce overhead (e.g., inlining a small println call).
	    - **Loop Unrolling**: Reducing loop overhead by duplicating loop body code.
	    - **Dead Code Elimination**: Removing unreachable or unused code.
	    - **Constant Folding**: Precomputing constant expressions (e.g., 2 + 3 becomes 5).
	    - **Branch Prediction**: Optimizing conditional branches based on observed execution paths.
	    - **Escape Analysis**: Determining if objects can be allocated on the stack instead of the heap to reduce garbage collection.
	- These optimizations are speculative, meaning they assume certain conditions (e.g., a method is always called with the same type). The JVM can **deoptimize** if assumptions fail.
6. **Execution of Native Code**:
	- The compiled native code is stored in the JVM’s **Code Cache**.
	- Subsequent calls to the compiled method execute the native code directly, bypassing the interpreter.
	- If the program’s behavior changes (e.g., a new class is loaded), the JVM may deoptimize and revert to interpretation or recompile with updated assumptions.

![[java-just-in-time-jit-compiler-overview.png]]
### Differences 
**JVM VS JDK**

| **Aspect**           | **JVM (Java Virtual Machine)**                                                                                                                                    | **JDK (Java Development Kit)**                                                                                                                               |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Definition**       | A virtual machine that executes Java bytecode, providing a platform-independent runtime environment.                                                              | A software development kit that provides tools, libraries, and the JRE for developing and running Java applications.                                         |
| **Primary Role**     | Executes compiled Java bytecode (.class files) by translating it to native machine code.                                                                          | Enables developers to write, compile, debug, and run Java programs.                                                                                          |
| **Components**       | - Class Loader<br>- Bytecode Verifier<br>- Execution Engine (Interpreter, JIT Compiler)<br>- Garbage Collector<br>- Runtime Data Areas (Heap, Stack, Method Area) | - JRE (includes JVM and core libraries)<br>- javac (compiler)<br>- java (runtime launcher)<br>- Tools (e.g., javadoc, jar, jdb)<br>- Standard Java libraries |
| **Scope**            | Runtime environment only; does not include development tools.                                                                                                     | Development and runtime environment; includes JVM, JRE, and development tools.                                                                               |
| **Usage**            | Used to run Java programs (e.g., java HelloWorld).                                                                                                                | Used to develop (write, compile) and run Java programs (e.g., javac HelloWorld.java, java HelloWorld).                                                       |
| **Dependency**       | Part of the JRE, which is included in the JDK.                                                                                                                    | Includes the JRE (and thus the JVM) as a subset.                                                                                                             |
| **Installation**     | Not installed standalone; comes with JRE or JDK.                                                                                                                  | Installed by developers; includes JRE and JVM.                                                                                                               |
| **Example Use Case** | Executes HelloWorld.class to print Hello World!.                                                                                                                  | Compiles HelloWorld.java to HelloWorld.class using javac and runs it using java.                                                                             |
| **Target Audience**  | End-users running Java applications (via JRE).                                                                                                                    | Developers building Java applications.                                                                                                                       |
| **Size**             | Smaller, as it’s a subset of JRE/JDK (focuses on execution).                                                                                                      | Larger, as it includes JVM, JRE, and development tools.                                                                                                      |

**JVM VS JRE**

|**Aspect**|**JVM (Java Virtual Machine)**|**JRE (Java Runtime Environment)**|
|---|---|---|
|**Definition**|A virtual machine that executes Java bytecode.|A package that includes the JVM, libraries, and runtime components to run Java applications.|
|**Function**|Runs Java code by converting bytecode to machine instructions.|Provides the complete environment (JVM + libraries) to run Java programs.|
|**Components**|Includes interpreter, JIT compiler, garbage collector, etc.|Includes JVM, Java Class Library, APIs, and other runtime files.|
|**Scope**|Core execution engine, a subset of JRE.|Broader package containing JVM and additional resources.|
|**Usage**|Executes bytecode; not directly installed alone.|Installed to run Java applications on a system.|
|**Standalone**|Not standalone; part of JRE or JDK.|Standalone package for running Java apps.|
|**Example Analogy**|Engine of a car.|Entire car (engine + fuel system + other components).|

**Interpreter VS Compiler**

|Aspect|Interpreter|Compiler|
|---|---|---|
|**Definition**|Translates and executes source code line-by-line (or statement-by-statement) at runtime.|Translates the entire source code into machine/target code before execution.|
|**Translation Unit**|One statement or line at a time.|The whole program (or large modules) as a single translation unit.|
|**Output**|No standalone output file; executes directly from source or intermediate representation.|Generates an executable or object file (machine code or bytecode).|
|**Execution Process**|Fetch → Decode → Execute for each line; repeats until program ends.|Full translation first, then a separate execution phase runs the produced binary.|
|**Error Detection**|Stops and reports errors as soon as it hits them during execution.|Reports all syntax/semantic errors during compilation; execution only if compilation succeeds.|
|**Performance**|Generally slower execution (overhead of on-the-fly translation).|Typically faster at runtime (no translation overhead once compiled).|
|**Memory Usage**|Lower memory footprint for translation, but keeps source in memory.|May require more memory for compiler data structures; runtime uses only compiled code.|
|**Platform Dependency**|Needs the interpreter installed on each platform.|Generated executable is platform-specific; needs recompilation for other platforms.|
|**Debugging**|Easier to debug interactively (can test snippets quickly).|Often uses separate debugging tools; harder to test partial changes without full recompile.|
|**Examples**|Python, Ruby, JavaScript, MATLAB|C, C++, Rust, Go; Java/Kotlin compile to bytecode, then interpreted/​JIT by JVM.|
|**Typical Use Cases**|Scripting, rapid prototyping, educational tools, REPL environments.|System software, performance-critical applications, large codebases.|
### Behind the scene of apk file generation



