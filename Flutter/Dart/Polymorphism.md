**Method overriding**
Method overriding is a technique in which we can create a method in the child class that has the same name as the method in the parent class. The method in the child class overrides the method in the parent class.
`Syntax`
```
class ParentClass{
void functionName(){
  }
}
class ChildClass extends ParentClass{
@override 
void functionName(){
  }
}
```

`Example of method overriding`
```
class Animal {
  void makeSound() {
    print("Some generic animal sound");
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Woof! Woof!");
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print("Meow! Meow!");
  }
}

void main() {
  Animal myDog = Dog();
  Animal myCat = Cat();

  myDog.makeSound(); // Output: Woof! Woof!
  myCat.makeSound(); // Output: Meow! Meow!
}
```

`Example of polymorphism with abstract class`
```
abstract class Shape {
  double getArea();
}

class Circle extends Shape {
  final double radius;
  Circle(this.radius);

  @override
  double getArea() => 3.14 * radius * radius;
}

class Rectangle extends Shape {
  final double width;
  final double height;
  Rectangle(this.width, this.height);

  @override
  double getArea() => width * height;
}

void printArea(Shape shape) {
  print("The area is: ${shape.getArea()}");
}

void main() {
  Shape circle = Circle(5);
  Shape rectangle = Rectangle(4, 6);

  printArea(circle);    // Output: The area is: 78.5
  printArea(rectangle); // Output: The area is: 24.0
}
```

`Example of polymorphism with interface`
```
class Printer {
  void printData();
}

class DocumentPrinter implements Printer {
  @override
  void printData() {
    print("Printing document data...");
  }
}

class PhotoPrinter implements Printer {
  @override
  void printData() {
    print("Printing photo data...");
  }
}

void printContent(Printer printer) {
  printer.printData();
}

void main() {
  Printer docPrinter = DocumentPrinter();
  Printer photoPrinter = PhotoPrinter();

  printContent(docPrinter);   // Output: Printing document data...
  printContent(photoPrinter); // Output: Printing photo data...
}
```

`Example of polymorphic variable`
```
class Employee {
  void work() {
    print("Working...");
  }
}

class Manager extends Employee {
  @override
  void work() {
    print("Managing the team");
  }
}

class Developer extends Employee {
  @override
  void work() {
    print("Writing code");
  }
}

void main() {
  List<Employee> employees = [Manager(), Developer()];

  for (var employee in employees) {
    employee.work();
  }
  // Output:
  // Managing the team
  // Writing code
}
```

`Why Use Polymorphism?`
1. **Code Reusability**: Polymorphism allows you to write generic functions that can work with objects of different types.
2. **Flexibility**: It enables flexibility by allowing a single interface to represent different underlying forms (subclasses).
3. **Maintainability**: Polymorphism reduces code duplication, making the codebase easier to maintain and extend.

`key points`
- *Polymorphism* in Dart allows objects of different classes to be treated as instances of a common superclass or interface.
- It is mainly achieved through *method overriding*, *abstract classes*, and *interfaces*.
- Polymorphism enables *dynamic method dispatch*, where the method call is resolved at runtime based on the actual object type.
- It improves code flexibility, reusability, and maintainability, making it a core principle of object-oriented programming in Dart.

**Operator overloading**
In dart, `operator oveloading` allows us to define how certain operators behave when applied to instances of your custom classes. This feature lets us use familiar operators like `+`, `-`, `*`, `/`, `==`, and others with our own classes, making the code more intuitive and readable.

`Key points`
- `Special methods`: `Opwrators` are defined using special methods with the `operator` keyword.
- `Limited set of methods`: Only specific set of operators can be overload in dart, such as `+`, `-`, `*`, `/`, `==`
- `Intuitive code`: operator overloading makes the use of custom classes more natural and similar to build in types.
- `Type safety`: Dart enforces type safety, so the result of an overload operator must return a valid type.

`Syntax`
```
class ClassName {
  ReturnType operator +(ParameterType other) {
    // Implementation
  }
}
```

`List of Operators You Can Overload in Dart`

|Operator|Method Name|
|---|---|
|`+`|`operator +`|
|`-`|`operator -`|
|`*`|`operator *`|
|`/`|`operator /`|
|`~/`|`operator ~/`|
|`%`|`operator %`|
|`==`|`operator ==`|
|`[]`|`operator []`|
|`[]=`|`operator []=`|
|`~`|`operator ~`|
|`<`|`operator <`|
|`>`|`operator >`|
|`<=`|`operator <=`|
|`>=`|`operator >=`|
|`-` (unary)|`operator -`|
|`!` (unary)|`operator !`|

`Example`
```
class Vector {
  final int x;
  final int y;

  Vector(this.x, this.y);

  // Overloading the '+' operator
  Vector operator +(Vector other) => Vector(x + other.x, y + other.y);

  // Overloading the '-' operator
  Vector operator -(Vector other) => Vector(x - other.x, y - other.y);

  // Overloading the '*' operator for scalar multiplication
  Vector operator *(int scalar) => Vector(x * scalar, y * scalar);

  // Overloading the '==' operator for equality comparison
  @override
  bool operator ==(Object other) =>
      other is Vector && x == other.x && y == other.y;

  // Overloading the '[]' operator for index access
  int operator [](int index) {
    if (index == 0) return x;
    if (index == 1) return y;
    throw IndexError(index, this, 'Index out of bounds');
  }

  // Overloading the '>' operator for comparison
  bool operator >(Vector other) => (x + y) > (other.x + other.y);

  // Overloading the '<' operator for comparison
  bool operator <(Vector other) => (x + y) < (other.x + other.y);

  // Overloading the 'unary -' operator
  Vector operator -() => Vector(-x, -y);

  // Overloading the 'toString' method for better string representation
  @override
  String toString() => 'Vector($x, $y)';

  // Overloading the 'hashCode' for consistency with '=='
  @override
  int get hashCode => Object.hash(x, y);
}

void main() {
  Vector v1 = Vector(2, 3);
  Vector v2 = Vector(1, 1);

  print('v1: $v1');
  print('v2: $v2');

  // Using overloaded '+' operator
  print('v1 + v2: ${v1 + v2}');

  // Using overloaded '-' operator
  print('v1 - v2: ${v1 - v2}');

  // Using overloaded '*' operator
  print('v1 * 3: ${v1 * 3}');

  // Using overloaded '==' operator
  print('v1 == v2: ${v1 == v2}');
  print('v1 == Vector(2, 3): ${v1 == Vector(2, 3)}');

  // Using overloaded '[]' operator
  print('v1[0]: ${v1[0]}, v1[1]: ${v1[1]}');

  // Using overloaded '>' and '<' operators
  print('v1 > v2: ${v1 > v2}');
  print('v1 < v2: ${v1 < v2}');

  // Using overloaded unary '-' operator
  print('-v1: ${-v1}');
}
```

`Caution with Operator Overloading`
- *Clarity*: Overusing operator overloading can make the code confusing if the operators are not used intuitively.
- *Performance*: Overloaded operators may introduce overhead, so use them judiciously in performance-critical applications.