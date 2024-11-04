Variable are containers used to store value in the program. There are different types of variables where you can keep different kinds of values.

**Types of variable**
- `String`: For storing text value, E.g(Name, Address, Phone number) etc.
- `Int`: For storing integer value E.g(10, -10, 8855) *Range*(-2<sup>63</sup> to 2<sup>63</sup> approximately *-9,223,372,036,854,775,808* to *9,223,372,036,854,775,807*))
- `double`: For storing decimal value E.g(10.1, 20.3). *Double* type is 64 bit floating point number 
	- Maximum range is *1.7976931348623157e+308*
	- Minimum range is *5e-324* (closest to zero, but still positive)
	- Negative range is similar to positive range but in a negative range *-1.7976931348623157e+308*  and *-5e-324*
- `bool`: For storing boolean type data E.g(true, false)
- `num`: For storing any type of number. E.g.(10, 20.2, -20) [both int and double]
- `var`: For storing any value. E.g. ‘Bimal’, 12, ‘z’, true. Dart compiler automatically infers the type of the variable based on the initial assigned value
- `const`: For storing constant value E.g(pie 3.14) compile time variable 
- `final`: For storing constant value E.g(pie 3.14) runtime variable

**String variable example**

`Basic declaration`
```
String greeting = 'Hello, Atik Faysal!'; //basic declaration of a string 
print(greeting); // Output: Hello, Atik Faysal!
```

`Var string declaration`
```
var message = 'Welcome to Dart programming';
print(message); // Output: Welcome to Dart programming
```

`Multiline string declaration`
```
  String multiLine = '''
This is a
multi-line
string.
''';
  print(multiLine);
// Output:
// This is a
// multi-line
// string.
```

`String Interpolation`
```
String name = 'Atik';
int age = 29;
String introduction = 'My name is $name and I am $age years old.';
print(introduction); // Output: My name is Atik and I am 29 years old.
```

`String concatation`
```
String part1 = 'Hello, ';
String part2 = 'world!';
String combined = part1 + part2;
print(combined); // Output: Hello, world!
```

`Row string`
- Prefixing a string with `r` makes it a raw string, which treats backslashes (`\`) as literal characters.
```
 String filePath = r'C:\Program Files\Dart';
 print(filePath); // Output: C:\Program Files\Dart
```

**Int variable example**

`Basic declaring`
```
int age = 25;
print(age); //output: 25
```

`Arithmetic Operations`
```
int length = 10;
int width = 5;
int area = length * width; // Multiplying two int variables
print("The area is $area"); // Output: The area is 50
```

`Conditional Statements`
```
int score = 85;
if (score > 50) {
  print("Passed");
} else {
  print("Failed");
}
// Output: Passed
```

**Double variable example**

`Basic declaration`
```
double height = 5.4;
print(height);//output: 5.4
```

`Arithmatic operation`
```
 double price = 19.99;
 double taxRate = 0.08; // 8% tax
 double totalCost = price + (price * taxRate);
 print("Total cost with tax: \$${totalCost}");
```

`Conditional statement`
```
double discount = 5.75;
double price = 20.00;

if (price > discount) {
  print("Price after discount: ${price - discount}");
} else {
  print("Discount cannot be applied.");
}
```

**bool variable example**

`Basic declaration`
```
bool isActive = true;
bool isComplete = false;
```

`Conditional statement`
```
bool isRaining = true;
bool isCold = false;

if (isRaining && isCold) {
  print('Wear a raincoat and a sweater.');
} else if (isRaining || isCold) {
  print('Take necessary precautions.');
} else {
  print('The weather is nice!');
}
// Output: Take necessary precautions.
```

**num variable example**

`Basic declaration`
```
// Declare a num variable and assign an integer value
num value = 10; 
print(value); // Output: 10 
// Reassign a double value to the same variable 
value = 10.5; 
print(value); // Output: 10.5
```

**var variable example**

`Basic declaration`
```
var name = 'Alice'; // Inferred as String 
var age = 30; // Inferred as int 
var isStudent = false; // Inferred as bool 

print(name); // Output: Alice 
print(age); // Output: 30 
print(isStudent); // Output: false
```

**const variable example**
>`const` is used to declare compile-time constants, meaning the variable’s value is determined at compile-time and cannot be changed afterward. A `const` variable is also immutable and is commonly used for values that should never change throughout the program's lifecycle.

`Basic declaration`
```
const int maxUsers = 100;
const String appName = "MyApp";
const double pi = 3.14159;

const List<String> colors = ['red', 'green', 'blue']; 
const Map<String, int> errorCodes = {'notFound': 404, 'serverError': 500}; 

void main() {
  print("Max users allowed: $maxUsers");
  print("App Name: $appName");
  print("Value of Pi: $pi");
  print(colors); // Output: [red, green, blue] 
  print(errorCodes); // Output: {notFound: 404, serverError: 500}
}
```

**final variable example**
>`final` is used to declare a variable whose value is set only once and cannot be modified afterward. The type of the variable can still be inferred or explicitly specified, but the assigned value remains constant after the initial assignment.

`Basic declaration`
```
final name = 'Alice'; // Type inferred as String
name = 'Bob'; // Error: Cannot assign a new value to a final variable

print(name); // Output: Alice

final int age = 25;
age = 30; // Error: Cannot assign a new value to a final variable

print(age); // Output: 25
```

**const vs final**
- `const` is for compile-time constants, while `final` is for runtime constants (variables that are assigned once and never changed).
- `const` can only be used if the value is known at compile time, while `final` can be assigned at runtime.
```
final currentDate = DateTime.now(); // Allowed, as it’s evaluated at runtime
// const compileTime = DateTime.now(); // Error, `const` can't be assigned at runtime
```
