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
