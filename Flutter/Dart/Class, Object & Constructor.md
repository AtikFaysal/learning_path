**Class**

>A class in Dart defines the properties (variables) and methods (functions) an object will have. It serves as a template for creating objects with similar characteristics.

`Example`
```
class Person {
  String name = '';
  int age = 0;

  void introduce() {
    print("Hi, I'm $name and I'm $age years old.");
  }
}
```

**Object**
>An object is an instance of a class. You create an object by using the `new` keyword (optional) or simply calling the class name.

`Example`
```
void main() {
  var person = Person(); // Creating an object of class Person
  person.name = 'Alice';
  person.age = 30;
  person.introduce(); // Output: Hi, I'm Alice and I'm 30 years old.
}
```

**Constructor**
>Constructors are special methods in a class used to initialize an object when it’s created. Dart provides both **default constructors** and **custom constructors**.

`Types of constructor`
- *Default constructor*
- *Generative constructor*
- *Named constructor*
- *Factory constructor*
- *Redirecting constructor*
- *Constant constructor*

`Default constructor`
>The constructor which is automatically created by compiler, if you don't create a constructor is called default constructor.

`Example`
```
class Person{  
  var name;  
  var age;  
  var address;  
  Person(){  
	 //this is a default constructor  
	 print("Hello person");  
  }  
}

void main(){  
  Person person = Person();
}
```

`Parameterized constructor`
>*Parameterized constructor* is used to initialize the instance variables of the class. Parameterized constructor is the constructor that takes parameters. It is used to pass the values to the constructor at the time of object creation.

`Example`
```
class Person {  
  var name;  
  var age;  
  var address;  
  Person(this.name, this.age, this.address);  
  
  void displayInfo() {  
    print("Person info: $name, $age, $address");  
  }}  
  
void main() {  
  Person person = Person("Atik", 29, "Dhaka");  
  
  person.displayInfo();  
}
```

`Named constructor`
>`Named constructor` allows to define multiple ways to create an object of a class. `Named constructor` is particularly use full when you need to initialize an object in different ways such as default values ore special configuration.

`Example`
```
class Person {  
  String userName;  
  int userId;  
  
  Person(this.userId, this.userName);  
  
  Person.fromJson(Map<String, dynamic> json)  
      : userName = json['username'],  
        userId = json['userid'];  
  
  void displayInfo() {  
    print("Welcome to our new memeber $userName($userId)");  
  }}  
  
void main() {  
  var person1 = Person(100, "Atik Faysal");  
  var jsonData = {'username':'Atik Faysal', 'userid': "101"};  
  var person2 = Person.fromJson(jsonData);  
  person1.displayInfo();  
  person2.displayInfo();  
}
```

`Constant constructor`
> `Constant constructor` is a constructor that is creates a constant object, whose value can not changed. A constant constructor is declared using the keyword `const`

`Condition of constant constructor`
- All properties of the class must be final
- It does not have any body
- Only class containing const constructor is initialized using the `const` keyword.

`Example`
```
class Point {
  final int x;
  final int y;

  const Point(this.x, this.y);
}

void main() {
  // p1 and p2 has the same hash code.
  Point p1 = const Point(1, 2);
  print("The p1 hash code is: ${p1.hashCode}");

  Point p2 = const Point(1, 2);
  print("The p2 hash code is: ${p2.hashCode}");
  // without using const
  // this has different hash code.
  Point p3 = Point(2, 2);
  print("The p3 hash code is: ${p3.hashCode}");

  Point p4 = Point(2, 2);
  print("The p4 hash code is: ${p4.hashCode}");
}
```