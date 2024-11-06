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
- *Generative constructor*
- *Default constructor*
- *Named constructor*
- *Factory constructor*
- *Redirecting constructor*
- *Constant constructor*
