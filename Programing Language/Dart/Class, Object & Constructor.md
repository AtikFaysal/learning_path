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

**Default constructor**
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

**Parameterized constructor**
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

**Named constructor**
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

**Constant constructor**
> `Constant constructor` is a constructor that is creates a constant object, whose value can not changed. A constant constructor is declared using the keyword `const`

`Condition of constant constructor`
- All properties of the class must be final
- It does not have any body
- Only class containing const constructor is initialized using the `const` keyword.
- Not possible to create multiple constant constructor.

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

`Use case of constant constructor`
- *UI design with predefined colors and styles*:
		In UI design we often use a set of predefined colors, text style, themes that remain constant throughout application. Constant constructors allow us to define these colors or styles once and use them everywhere without creating new instances.
``` 
class AppColors {
  final int red;
  final int green;
  final int blue;

  // Constant constructor
  const AppColors(this.red, this.green, this.blue);

  // Predefined color constants
  static const AppColors primaryColor = AppColors(0, 128, 255);
  static const AppColors accentColor = AppColors(255, 165, 0);
  static const AppColors backgroundColor = AppColors(240, 240, 240);
}
```
- *Constant configuration data*
		If application has configuration setting or predefined data values, like API endpoints, version numbers, or feature flags, constant constructors allows to define these immutable, compile time constants. This ensure that the configuration values are accessible globally and can not be modified.
```
class Config {
  final String apiEndpoint;
  final String version;

  // Constant constructor
  const Config(this.apiEndpoint, this.version);

  // Static constant instances for environments
  static const Config dev = Config('https://dev.api.com', '1.0.0');
  static const Config prod = Config('https://api.com', '1.0.0');
}
```
- *Representing finite states in state management*
		In state management pattern, we may have fixed states, such a s `Loading`, `Success`, `Error`, that don't change. Using constant constructors for these states avoid creating new instances each time, which can lead to optimized memory usage.
```
class NetworkState {
  final String message;

  const NetworkState._(this.message);

  // Predefined constant instances for each state
  static const NetworkState loading = NetworkState._('Loading...');
  static const NetworkState success = NetworkState._('Success');
  static const NetworkState error = NetworkState._('An error occurred');
}
```
- *Immutable data models*
		For applications that rely one a fixed set of data models or constants(Country code, status code etc), constant constructors are useful for defining immutable instances that can be reused without creating duplicates.
```
class Country {
  final String name;
  final String code;

  const Country(this.name, this.code);

  // Constant instances of common countries
  static const Country usa = Country('United States', 'US');
  static const Country canada = Country('Canada', 'CA');
  static const Country india = Country('India', 'IN');
}

void main() {
  print(Country.usa.name); // Output: United States
}
```
- *Caching expensive immutable object*
		If a class represents an object with data that is expensive to initialize or compute but immutable(e.g. mathematical constants, unit conversions factors), a constant constructor can ensure the object is created once and reused.
```
class Constants {
  static const double pi = 3.14159;
  static const double gravity = 9.81;
  static const double speedOfLight = 299792458; // m/s
}

void main() {
  print(Constants.pi);          // Output: 3.14159
  print(Constants.gravity);      // Output: 9.81
  print(Constants.speedOfLight); // Output: 299792458
}
```

**Factory constructor**
> Factory constructor provide a way to create an instances of a class, but with more control than traditional constructors. A factory constructor does not always create a new instances, instead of creating new instance it can return an existing instance, a singleton, or even an instance of a subtype. This is particularly useful for implementing design patterns like singletons, caching, and object pooling.

`Syntax`
```
class ClassName {
  factory ClassName() {
    // Initialization logic
    return someInstance;
  }
}
```

`Example`
```
//factory constructor 
class User{  
  String? name;  
  User(this.name);  
  factory User.newUser(String name){  
    return User(name);  
  }}  
  
class Doctor extends User{  
  Doctor(String name) : super("Dr. $name");  
}
```

`Use case of factory constructor`
- *Singleton pattern*
		Singleton pattern ensure that, a class has only one instance throughout the application's lifecycle. You can use a factory constructor to implement a singleton.
```
class Database {
  // Private static variable to hold the singleton instance
  static final Database _instance = Database._internal();

  // Private named constructor
  Database._internal();

  // Factory constructor that returns the same instance every time
  factory Database() {
    return _instance;
  }

  void query(String sql) {
    print('Executing query: $sql');
  }
}

void main() {
  var db1 = Database();
  var db2 = Database();

  print(identical(db1, db2)); // Output: true (both are the same instance)
}
```
- *Caching instances*
		A factory constructor can also be used to cache instances based on specific criteria. For example we may want to cache instances of a class to avoid creating duplicate objects with the same value.
```
class Color {
  final int red;
  final int green;
  final int blue;

  // Cache to store instances
  static final Map<String, Color> _cache = {};

  // Factory constructor that caches instances
  factory Color(int red, int green, int blue) {
    final key = '$red,$green,$blue';

    if (_cache.containsKey(key)) {
      return _cache[key]!;
    } else {
      final color = Color._internal(red, green, blue);
      _cache[key] = color;
      return color;
    }
  }

  // Private named constructor
  Color._internal(this.red, this.green, this.blue);
}

void main() {
  var color1 = Color(255, 0, 0);
  var color2 = Color(255, 0, 0);
  
  print(identical(color1, color2)); // Output: true (cached instance)
}
```
- *Returning different types base on condition*
		A factory constructor can return instances of different subclasses or implementations based on conditions. This is useful for creating a class hierarchy with different behaviors.
```
abstract class Shape {
  factory Shape(String type) {
    if (type == 'circle') return Circle();
    if (type == 'rectangle') return Rectangle();
    throw 'Unknown shape type';
  }

  void draw();
}

class Circle implements Shape {
  @override
  void draw() {
    print('Drawing a circle');
  }
}

class Rectangle implements Shape {
  @override
  void draw() {
    print('Drawing a rectangle');
  }
}

void main() {
  var shape1 = Shape('circle');
  var shape2 = Shape('rectangle');

  shape1.draw(); // Output: Drawing a circle
  shape2.draw(); // Output: Drawing a rectangle
}
```

**Private constructor**
>The private constructor is an constructor that can only be accessed within its class. This is important in situations like implementing the singleton pattern. 

`Example`
```
class Example {
  // Private constructor
  Example._();

  // Public factory constructor that provides controlled access
  factory Example.instance() {
    return Example._();
  }
}
```

`Use case of private constructor`
- *Singleton pattern*
		A common use of private constructor is implementing the singleton pattern, which is ensures that only one instance of a class created.
```
class Singleton {
  // The single instance
  static final Singleton _instance = Singleton._internal();

  // Private named constructor
  Singleton._internal();

  // Factory constructor that returns the single instance
  factory Singleton() {
    return _instance;
  }

  void showMessage() {
    print("Singleton instance accessed");
  }
}

void main() {
  var instance1 = Singleton();
  var instance2 = Singleton();

  print(identical(instance1, instance2)); // Output: true (same instance)
}
```
- *Prevent instantiation*
		if a class is meant to be a utility class(like `Math` or `Constants`) and should never be instantiated, a private constructor can prevent instantiation.
```
class MathUtils {
  // Private constructor to prevent instantiation
  MathUtils._();

  static double square(double num) => num * num;
  static double cube(double num) => num * num * num;
}

void main() {
  print(MathUtils.square(3)); // Output: 9
  // MathUtils utils = MathUtils(); // Error: The constructor is private
}
```
- *Internal constructors for factory patterns*
		A private constructor is often used along with a public factory constructor to return instances based on specific conditions, while keeping the actual creation logic hidden.
```
class User {
  final String name;
  final int age;

  // Private named constructor
  User._(this.name, this.age);

  // Factory constructor that returns instances based on conditions
  factory User.createUser(String name, int age) {
    if (age >= 18) {
      return User._(name, age);
    } else {
      throw ArgumentError("User must be at least 18 years old.");
    }
  }
}

void main() {
  var adultUser = User.createUser("Alice", 30);
  print("User: ${adultUser.name}, Age: ${adultUser.age}");

  // var minorUser = User.createUser("Bob", 16); // Error: User must be at least 18 years old.
}
```

**Redirecting constructor**
>The redirecting constructor is a constructor that calls another constructor of the same class. Especially, using this type of constructor can improve reusability and readability as well as the reliability of the code.

`Example`
```
class Person {  
  String? name;  
  String? job;  
  
  Person(this.name, this.job);  
  
  Person.doctor(name): this(name, 'Doctor');  
}
```

` Rules for Redirecting Constructors`
1. *Only One Target Constructor*: A redirecting constructor can only redirect to one other constructor. You cannot chain multiple redirecting constructors.
2. *No Additional Body*: Redirecting constructors cannot have a body. All initialization must be handled by the constructor they are redirecting to.
3. *Use of Initializer List*: You can add an initializer list before redirecting, but you cannot use both an initializer list and a constructor body.

`Use case of redirecting constructor`
- *Provide default value for specific constructor*
		In many scenarios, we might want to initialize an object with a set of default values, but without duplicating the initialization logic. A redirecting constructor lets us create alternative constructors with default values while delegating the actual initialization to the main constructor.
```
class UserProfile {
  final String name;
  final String email;
  final String role;

  // Main constructor
  UserProfile(this.name, this.email, this.role);

  // Redirecting constructor for regular user
  UserProfile.regularUser(String name, String email) : this(name, email, 'user');

  // Redirecting constructor for admin user
  UserProfile.admin(String name, String email) : this(name, email, 'admin');
}

void main() {
  var user = UserProfile.regularUser('Alice', 'alice@example.com');
  var admin = UserProfile.admin('Bob', 'bob@example.com');

  print('${user.name}, ${user.role}'); // Output: Alice, user
  print('${admin.name}, ${admin.role}'); // Output: Bob, admin
}
```
- `Simplifying complex initializing`
		Redirecting constructors can help simplify complex initialization by breaking down the process into different constructors that call the main constructor with pre-set configurations.
```
class Shape {
  final double width;
  final double height;

  // Main constructor for custom shapes
  Shape(this.width, this.height);

  // Redirecting constructor for squares
  Shape.square(double side) : this(side, side);

  // Redirecting constructor for rectangles with predefined dimensions
  Shape.standardRectangle() : this(10.0, 20.0);
}

void main() {
  var square = Shape.square(5.0);
  var rectangle = Shape.standardRectangle();

  print('Square: ${square.width} x ${square.height}'); // Output: Square: 5.0 x 5.0
  print('Rectangle: ${rectangle.width} x ${rectangle.height}'); // Output: Rectangle: 10.0 x 20.0
}
```
- *Enhanced readability for alternative constructor*
		When we have multiple ways to create an instance of a class, each with slightly different inputs or default values, redirecting constructors help improve readability. They provide named alternatives that make it clear what type of instance is being created.
```
class Event {
  final String name;
  final DateTime startTime;

  // Main constructor for a specific date and time
  Event(this.name, this.startTime);

  // Redirecting constructor for events starting today
  Event.today(String name) : this(name, DateTime.now());

  // Redirecting constructor for events starting tomorrow
  Event.tomorrow(String name) : this(name, DateTime.now().add(Duration(days: 1)));
}

void main() {
  var eventToday = Event.today('Meeting');
  var eventTomorrow = Event.tomorrow('Workshop');

  print('Event Today: ${eventToday.startTime}');
  print('Event Tomorrow: ${eventTomorrow.startTime}');
}
```
- *Enforcing consistent initialization logic*
		Redirecting constructors can enforce consistent initialization logic, ensuring that all constructors funnel through the main constructor, which centralizes how instances are created and avoids inconsistent setups.
```
class BankAccount {
  final String accountHolder;
  final double balance;
  final double withdrawalLimit;

  // Main constructor with all parameters
  BankAccount(this.accountHolder, this.balance, this.withdrawalLimit);

  // Redirecting constructor with a default withdrawal limit
  BankAccount.withDefaultLimit(String accountHolder, double balance)
      : this(accountHolder, balance, 1000.0);
}

void main() {
  var account1 = BankAccount('Alice', 5000.0, 2000.0);
  var account2 = BankAccount.withDefaultLimit('Bob', 3000.0);

  print('Account 1: ${account1.withdrawalLimit}'); // Output: Account 1: 2000.0
  print('Account 2: ${account2.withdrawalLimit}'); // Output: Account 2: 1000.0
}
```

**Generative constructor**
>`Generative constructor` is the standard constructor used to create a new instance of a class. It is the most commonly used constructor type in Dart, allowing you to initialize properties of an object, perform setup logic, and create an entirely new instance. Generative constructors differ from factory constructors in that they always return a new instance of the class, rather than potentially reusing an existing instance.

`Syntax`
```
class ClassName {
  ClassName(parameters) {
    // Initialization or setup logic
  }
}
```

`Example`
```
class Person {
  String name;
  int age;

  // Generative constructor
  Person(this.name, this.age);

  void introduce() {
    print("Hi, I'm $name and I'm $age years old.");
  }
}

void main() {
  var person = Person('Alice', 25);
  person.introduce(); // Output: Hi, I'm Alice and I'm 25 years old.
}
```

`Use case of generative constructor`

- *Initializing immutable data models*
		In applications where we work with data models, like a user profile or a product, we might need to create instances with fixed, immutable data. Generative constructors allow you to initialize these models with specific data while ensuring immutability through `final` fields.
```
class UserProfile {
  final String username;
  final String email;
  final DateTime createdAt;

  // Generative constructor
  UserProfile(this.username, this.email) : createdAt = DateTime.now();
}

void main() {
  var user = UserProfile('alice', 'alice@example.com');
  print('User: ${user.username}, Email: ${user.email}, Created At: ${user.createdAt}');
}
```
- *Setting default values*
		Generative constructor allow us to set default values for fields, which is helpful when certain properties need to start with standard values. This is common in UI configurations, where default settings or options need to be pre-configured.
```
class ButtonConfig {
  final String label;
  final String color;
  final double size;

  // Generative constructor with default values
  ButtonConfig(this.label, {this.color = 'blue', this.size = 14.0});
}

void main() {
  var defaultButton = ButtonConfig('Click Me');
  var customButton = ButtonConfig('Submit', color: 'red', size: 16.0);

  print('Default Button: ${defaultButton.label}, Color: ${defaultButton.color}, Size: ${defaultButton.size}');
  print('Custom Button: ${customButton.label}, Color: ${customButton.color}, Size: ${customButton.size}');
}
```
- *Input validation*
		Generative constructions are commonly used to validate input data before an object s created. This helpful for ensuring that an object always has a valid state upon creation, which can prevent runtime errors and improve data integrity.
```
class BankAccount {
  final String accountHolder;
  final double balance;

  // Generative constructor with validation
  BankAccount(this.accountHolder, this.balance) {
    if (balance < 0) {
      throw ArgumentError('Balance cannot be negative');
    }
  }
}

void main() {
  try {
    var account = BankAccount('Alice', 500.0);
    print('Account created with balance: ${account.balance}');

    var invalidAccount = BankAccount('Bob', -100.0); // This will throw an error
  } catch (e) {
    print('Error: $e'); // Output: Error: Invalid argument(s): Balance cannot be negative
  }
}
```
- *Computing properties on initialization*
		Sometimes, certain properties of an object are derived from the input parameters. A generative constructor with an initializer list can be used to compute these properties, setting them to calculated values when the object is created.
```
class Circle {
  final double radius;
  final double circumference;
  final double area;

  // Generative constructor with initializer list for computed properties
  Circle(this.radius)
      : circumference = 2 * 3.14 * radius,
        area = 3.14 * radius * radius;
}

void main() {
  var circle = Circle(5.0);
  print('Radius: ${circle.radius}, Circumference: ${circle.circumference}, Area: ${circle.area}');
}
```
- *Implementing multiple constructors with different parameters*
		Generative constructors allow to create multiple constructors for initializing an object with different parameters. This is often used in cases where we want flexible initialization options.
```
class Rectangle {
  final double width;
  final double height;

  // Main constructor
  Rectangle(this.width, this.height);

  // Named constructor for a square
  Rectangle.square(double side) : width = side, height = side;
}

void main() {
  var rectangle = Rectangle(10.0, 20.0);
  var square = Rectangle.square(15.0);

  print('Rectangle: ${rectangle.width} x ${rectangle.height}');
  print('Square: ${square.width} x ${square.height}');
}
```
- *Dependency injection with required parameter*
		For dependency injection, generative constructors are often used to require necessary parameters. This ensures that all required dependencies are provided at instantiation, avoiding null values and improving dependency management.
```
class Service {
  void performAction() {
    print('Action performed');
  }
}

class Controller {
  final Service service;

  // Generative constructor with required dependency
  Controller(this.service);

  void execute() {
    service.performAction();
  }
}

void main() {
  var service = Service();
  var controller = Controller(service);
  controller.execute(); // Output: Action performed
}
```