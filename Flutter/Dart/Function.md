`Syntax`
```
returntype functionName(parameter1,parameter2, ...){
  // function body
}
```

`Example`
```
//function that calculate interest
void calculateInterest(double principal, double rate, double time) {
  double interest = principal * rate * time / 100;
  print("Simple interest is $interest");
}

void main() {
  double principal = 5000;
  double time = 3;
  double rate = 3;
  calculateInterest(principal, rate, time);
}
```

`Types of function`
- No Parameter And No Return Type
- Parameter And No Return Type
- No Parameter And Return Type
- Parameter And Return Type

`No parameter and no return type`
```
void main() {
  printName();
}

void printName() {
  print("My name is John Doe.");
}
```

`Parameter & no return type`
```
// This function add two numbers
void add(int a, int b) {
  int sum = a + b;
  print("The sum is $sum");
}

void main() {
  int num1 = 10;
  int num2 = 20;

  add(num1, num2);
}
```

`No parameter & return type`
```
void main() {
// Function With No Parameter & Return Type
  String name = primeMinisterName();
  print("The Name from function is $name.");
}
String primeMinisterName() {
  return "John Doe";
}
```

`Parameter & return type`
```
//function that calculate interest
double calculateInterest(double principal, double rate, double time) {
  double interest = principal * rate * time / 100;
  return interest;
}

void main() {
  double principal = 5000;
  double time = 3;
  double rate = 3;
  double result = calculateInterest(principal, rate, time);
  print("The simple interest is $result.");
}
```

`Positional optional parameters`
```
void main() {
  print(fullName("Atik","Faysal","Engineer"));
  print(fullName("Atik","Faysal"));
}

String fullName(String firstName, String lastName, [String? title]){
  if(title != null)
    return "$firstName $lastName $title";
  else return "$firstName ($lastName)";
}
```

`Positional optional parameter with default value`
```
void describe(String name, [int age = 0, String city = 'Unknown']) {
  print('$name is $age years old and lives in $city.');
}

void main() {
  describe('Alice');                // Alice is 0 years old and lives in Unknown.
  describe('Bob', 25);              // Bob is 25 years old and lives in Unknown.
  describe('Charlie',30,'Paris'); // Charlie is 30 years old and lives in Paris.
}
```

`Named optional parameter with default value`
```
void displayUser({required String name, int age = 18}) {
  print('Name: $name, Age: $age');
}

void main() {
  displayUser(name: 'Atik');  // Name: Atik, Age: 18
  displayUser(name: 'Atik', age: 20);  // Name: Atik, Age: 20
  //displayUser();            // Error: The parameter 'name' is required
}
```

`Named parameter required`
```
void displayUser({required String name, int age = 18}) {
  print('Name: $name, Age: $age');
}

void main() {
  displayUser(name: 'Alice');  // Name: Alice, Age: 18
  // displayUser();            // Error: The parameter 'name' is required
}
```

`Optional types`
>Dart is an optionally-typed language, so it's possible to omit the types from function declaration. 

```
String getMessage(int number){
  return "$number is a number";
}

void main() {
  print(getMessage(10));
}
```

- Above function we can write like this
```
getMessage(number){
  return "$number is a number";
}

void main() {
  print(getMessage(10));
}
```

`Arrow functions`
>Dart has special syntax for functions whose body is only one line. Consider the following function named `add` that adds two numbers together: 

`Syntax`
```
ReturnType FunctionName(Parameters...) => Expression;
```

```
int add(int a, int b){
  return a + b;
}

void main() {
  print(add(10,20));
}
```

- Since the body is only one line, you can convert it to the following from:
```
int add(int a, int b)=> a + b;
```

`Anonymous function`
`Syntax`
```
(parameterList){
// statements
}
```

`Example`
```
void main() {
// Anonymous function
  var cube = (int number) {
    return number * number * number;
  };

  print("The cube of 2 is ${cube(2)}");
  print("The cube of 3 is ${cube(3)}");
}
```

`Extension function`
>**extension functions** allow you to add new methods or properties to existing classes without modifying their source code.
```
extension <extension name>? on <type> {  
(<member definition>)*  
}
```

`Example`
```
extension StringExtensions on String {
  String capitalize() {
    if (this.isEmpty) return this;
    return this[0].toUpperCase() + this.substring(1);
  }
}

void main() {
  String name = "dart";
  print(name.capitalize()); // Output: Dart
}
```

`Example`
```
extension ListExtensions on List<int> {
  int get sum => this.fold(0, (prev, element) => prev + element);
}

void main() {
  List<int> numbers = [1, 2, 3, 4];
  print(numbers.sum); // Output: 10
}
```

`Higher order function`
> **Higher-order function** is a function that can take other functions as parameters or return a function as a result. Higher-order functions are useful for creating flexible and reusable code, as they allow you to abstract functionality and pass behaviors dynamically.

`Pasing a function as an argument`
```
void printResult(int a, int b, int Function(int, int) operation) {
  int result = operation(a, b);
  print("The result is $result");
}

int add(int x, int y) => x + y;
int multiply(int x, int y) => x * y;

void main() {
  printResult(3, 4, add);       // Output: The result is 7
  printResult(3, 4, multiply);  // Output: The result is 12
}
```

`Return a function from another function`
```
Function(int) makeAdder(int x) {
  return (int y) => x + y;
}

void main() {
  var addFive = makeAdder(5);
  print(addFive(3)); // Output: 8
  print(addFive(10)); // Output: 15
}
```

`Callback function example`
```
void performOperation(int a, int b, Function(int, int) callback) {
  int result = a + b;
  callback(result, b);
}

void printOperation(int result, int value) {
  print("Result with $value is: $result");
}

void main() {
  performOperation(10, 5, printOperation); // Output: Result with 5 is: 15
}
```