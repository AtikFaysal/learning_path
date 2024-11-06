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