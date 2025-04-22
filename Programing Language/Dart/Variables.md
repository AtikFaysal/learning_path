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
- `dynamic`: For storing any kind of value, and allow to change the type of the value assigned to it.
- `Object`: For storing any kind of value like dynamic, but we can't directly call methods on an *Object* variable without type casting, as it doesn't bypass type check.

**String variable example**

`Basic declaration`
```
void main() {   
   String text1 = 'Example of a single-line string.';   
   String text2 = "Example of a single line string using double quotes.";   
   String text3 = """This is a multiline line   
string using the triple-quotes.
This is tutorial on dart strings.
""";   
   print(text1);  
   print(text2);   
   print(text3);   

	//output
	//Example of a single-line string.
	//Example of a single line string using double quotes.
	//This is a multiline line   
	//string using the triple-quotes.
	//This is tutorial on dart strings.
}
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

**dynamic**
>`dynamic` type is a special type that can hold any kind of value and allow to change the type of the value assigned to it. When a variable is declared with the `dynamic` type, it bypasses Dart's type checking, meaning we can assign values of any type to it at runtime

`Example`
```
void main() {
	dynamic value = 'Hello';  // Initially a String
	print(value);             // Output: Hello
	  
	value = 42;               // Now an int
	print(value);             // Output: 42
	  
	value = true;             // Now a bool
	print(value);             // Output: true

	printValue('Hello'); // Output: The value is Hello 
	printValue(42); // Output: The value is 42 
	printValue(true); // Output: The value is true
}

void printValue(dynamic value) { 
	print('The value is $value'); 
}
```

**Object**
>`Object?` is the root of all types in Dart, and like `dynamic`, it can hold any type of value. However, unlike `dynamic`, you can’t directly call methods on an `Object?` variable without casting, as it doesn’t bypass type checks.

`Example`
```
Object? value = 'Hello';
print((value as String).length); // Safe with casting
```

**Records**
> `records` allow to group multiple values together without creating a custom class. It's useful for holding related data in a lightweight and concise way. `recors` can be used as parameters in functions, making it easy to pass grouped values.

`record as parameter`
```
//positional record parameter  
(String, int, double) record;  
record = ("Atik", 29, 5.4);//position matters  
//record1 = (29, "Atik", 5.4); //Wrong  
  
(int a, int b) recordA = (1, 2);  
(int x, int y) recordX = (3, 4);  
recordA = recordX; // OK.  
  
//named record parameter  
({String name, int age, double height}) person;  
person = (age: 29, name: "Atik", height: 5.4);//Right, parameter position doesn't matter here  
  
({int a, int b}) recordAB = (a: 1, b: 2);  
({int x, int y}) recordXY = (x: 1, y: 2);  
  
//recordXY = recordAB;// Compile error! These records don't have the same type.  
print(recordXY == recordAB);//output false  
  
var recordFields = ('first', a: 2, b: true, 'last');  
  
print(recordFields.$1); // Prints 'first'  
print(recordFields.a); // Prints 2  
print(recordFields.b); // Prints true  
print(recordFields.$2); // Prints 'last'
```

`Example: positional record as parameter`
```
void main(){  
  var record = ("Atik", 29);  
  positionalRecordParameter(record);  
}

void positionalRecordParameter((String, int) record){  
  print("Name: ${record.$1} and age: ${record.$2}");  
}
```

`Example: Named record as parameter`
```
void main(){  
  var record = (name: "Atik", age: 29);  
   var record = ("Atik", 29); //Wrong 
  namedRecordParameter(record);  
}

void namedRecordParameter(({String name, int age}) record){  
  print("Name: ${record.name} and age: ${record.age}");  
}
```

`Example: Mixed(Named & Positional) parameter`
```
void main(){   
  var record = ("Hello: ", (name: "Atik Faysal", age: 30), "Dhaka");  
  mixedNamedPositionalParameter(record);  
}

void mixedNamedPositionalParameter((String, ({String name, int age}), String) record) {  
  // Accessing fields in the record  
  var first = record.$1; // First positional element (String)  
  var namedName = record.$2.name; // Named parameter 'name' in the second element  
  var namedAge = record.$2.age; // Named parameter 'age' in the second element  
  var third = record.$3; // Last positional element (String)  
  
  print('First: $first, Name: $namedName, Age: $namedAge, Third: $third');  
}
```

`Return a Mixed record`
```
(String, ({String name, int age}), String) returnMixedRecord(){  
  var record = ("Hello: ", (name: "Atik Faysal", age: 30), "Dhaka");  
  return record;  
}

void main() {
  var record = returnMixedRecord();  
  print('First: ${record.$1}, Name: ${record.$2.name}, Age: ${record.$2.age}, Third: ${record.$3}');
}
```

**Null safety**
> `Null safety` is a feature that helps prevent null reference errors, making code more robust and reducing runtime error.

`Non-Nullable types`: By default all variable is non null
```
int number = 5;
//number = null; //this is wrong and null safety prevent this
```

`Nullable types`: To declare a nullable variable add `?` after the data type. This indicates that the variable may hold a null value.
```
int? number = 10;
String? name = "Atik";
number = null;//Allowed because of the ? suffix
```

`Late keywords`: `late` keyword is used to tell that a non nullable variable will assigned later, but must assigned before it is accessed. This is useful when a variable can not be initialized at the time of declaration.
```
void main() {
  late int number;
  number = 10;
  print(number);
}
```

**Null aware operators**
`(?.)` `Null aware access`: Calls a method or access a property only if the object is non-null
```
String? name = "atik";
print(name?.length);//Print null instead of throwing an error
```

`(??) if null operator`: Provides a default value if the left side operand is null.
```
  String? name;
  print(name ?? "Atik faysal");
```

`(??=) if null assignment`: Assign a value only if the variable is currently null
```
  String? name;
  name ??= "Atik";
  print(name);
```

`(!) null assertion`: A nullable variable is non-null at this point. Use this carefully as it can lead to runtime errors if the variable is actually null.
```
  String? name = "Atik";
  print(name!);
}
```

`Example: Null safety in functions`:
```
void greet(String? name) {
  print('Hello, ${name ?? 'Guest'}');
}

void main() {
  greet(null);  // Output: Hello, Guest
  greet('Alice'); // Output: Hello, Alice
}
```

`Example: Null values in collections`:
```
void main() {
  List<int?> nullableList = [1, 2, null, 4]; // List of nullable integers
  List<int> nonNullableList = [1, 2, 3, 4]; // List of non-nullable integers
}
```
