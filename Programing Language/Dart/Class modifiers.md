**Abstract class & interface**
>In dart `abstract` class and interface are used to define a common structure and behavior for multiple classes. While they share similarities, they serve different purposes and have distinct characteristics. 

`Abstract class`
An `abstract class` is a class that can not be instantiated directly. It's used to define a blueprint for other classes, specifying method an properties that subclasses must implemented. An `abstract class` may have both `abstruct method` and `concrete method`. A concrete subclass must implement all `abstruct methods` and can optionally override concrete methods.

`Key points`
- Can not be instantiated directly.
- Can contain abstract method.
- Can contain concrete method.
- Used to define common interface and shared behavior for subclass.

`Example`

```
abstract class PaymentMethod {
  void processPayment(double amount);

  void refundPayment(double amount) {
    // Default implementation for refund
    print("Refunding \$${amount} using default method.");
  }
}
```

```
class CreditCardPayment extends PaymentMethod {
  @override
  void processPayment(double amount) {
    print("Processing credit card payment of \$${amount}");
  }
}

class PayPalPayment extends PaymentMethod {
  @override
  void processPayment(double amount) {
    print("Processing PayPal payment of \$${amount}");
  }
}

class BankTransferPayment extends PaymentMethod {
  @override
  void processPayment(double amount) {
    print("Processing bank transfer payment of \$${amount}");
  }
}
```

```
void main() {
  PaymentMethod payment1 = CreditCardPayment();
  payment1.processPayment(100.0);

  PaymentMethod payment2 = PayPalPayment();
  payment2.processPayment(200.0);

  PaymentMethod payment3 = BankTransferPayment();
  payment3.processPayment(150.0);

  payment1.refundPayment(50.0); // Uses the default refund implementation
}
```

`Abstract interface`
In dart, every class can act as an interface. There is no separate keywords for defining an interface. By default, when you implement a class, you are using it as an interface. `Interface` is a set of methods that class must implement in order to conform to that interface. It doesn't contain any implementations of its own, but simply defines the required methods that must be implemented. A class can implement multiple interfaces, allowing it to be used in different contexts as needed. 

`Key points`
- Any class in dart can be used as interface
- Interface define a concrete that the implementing class must fulfill. 
- When a class implements an interface, it must override all methods and properties declared by the interface.

`Example`
```
abstract class Payment {
  void processPayment(double amount);
  void refundPayment(double amount);
}
```

```
class CreditCardPayment implements Payment {
  @override
  void processPayment(double amount) {
    print('Processing credit card payment of \$${amount.toStringAsFixed(2)}');
  }

  @override
  void refundPayment(double amount) {
    print('Refunding credit card payment of \$${amount.toStringAsFixed(2)}');
  }
}

class PayPalPayment implements Payment {
  @override
  void processPayment(double amount) {
    print('Processing PayPal payment of \$${amount.toStringAsFixed(2)}');
  }

  @override
  void refundPayment(double amount) {
    print('Refunding PayPal payment of \$${amount.toStringAsFixed(2)}');
  }
}

class BitcoinPayment implements Payment {
  @override
  void processPayment(double amount) {
    print('Processing Bitcoin payment of \$${amount.toStringAsFixed(2)}');
  }

  @override
  void refundPayment(double amount) {
    print('Refunding Bitcoin payment of \$${amount.toStringAsFixed(2)}');
  }
}
```

```
void main() {
  Payment payment = CreditCardPayment();
  payment.processPayment(100.0);
  payment.refundPayment(50.0);

  payment = PayPalPayment();
  payment.processPayment(200.0);
  payment.refundPayment(100.0);

  payment = BitcoinPayment();
  payment.processPayment(300.0);
  payment.refundPayment(150.0);
}
```

**Base**
In dart `base` keyword is used to declare a base class that can only be extended, not implemented or mixed in. This feature is part of dart's enhanced type system, providing more control over inheritance and subclassing. It helps prevent unintended use of a class as an interface or mixin and ensures that the class is only used in inheritance chains.

`Key points`
- *Inheritance only*: A class marked as `base` can only be extended by other classes. It can not be used with `implementes` or `with`.
- *Prevent misuse*: The `base` keywords prevents the class from being used as an inheritance via `implement` and `with`.
- *Enhanced control*: It gives more control to library authors by explicitly defining how a class should be used.

`Example`
```
base class Vehicle {
  void move() {
    print("Vehicle is moving");
  }
}

class Car extends Vehicle {
  @override
  void move() {
    print("Car is driving");
  }
}

// Invalid code (uncommenting these lines will cause errors)
// class Bike implements Vehicle {}
// class Truck with Vehicle {}

void main() {
  var car = Car();
  car.move(); // Output: Car is driving
}
```

`Use case of base class`
1. *Library Design*: When designing a library, you may want certain classes to only be extended but not implemented or used as mixins. The `base` keyword enforces this restriction.
2. *Strict Inheritance Control*: The `base` keyword helps ensure that a class is only used in specific inheritance hierarchies, preventing misuse.
3. *Preventing Unintended Implementation*: It prevents other developers from implementing the class as an interface, which could lead to unintended usage patterns.

**Final**
In dart, `final` class modifier is used to declare a class that can not be subclassed(extended). It provides a way to prevent inheritance, ensuring that a class is not extended by any other class. This feature is useful when you want to make a class immutable in terms of its inheritance, similar to how the `final` keyword works for variables.

`Key points`
- *Preventing sub class*: A class marked as `final` can not be extended by any other class.
- *Encapsulation*: It enforces encapsulation by restricting inheritance, which can be useful in scenarios where you ensure that a class's behavior remains unchanged. 
- *Immutable behavior*: It helps in creating classes with immutable behavior, similar to how `final` variables can not be reassigned.

`Example`
```
final class Vehicle {
  void drive() {
    print("Vehicle is driving");
  }
}

class Car extends Vehicle {} // Error: 'Vehicle' can't be extended because it's a final class.

void main() {
  var vehicle = Vehicle();
  vehicle.drive(); // Output: Vehicle is driving
}
```

**Sealed**
In dart, a sealed class is a special type of class that restricts which class can extend or implement. Only classes defined in the same file can extend or implement a sealed class. 
This feature allows you to define a base class with a finite set of subclasses, making your code more predictable and safer, as all possible subclasses are known at compile time.

`Key points`
- *Restricted subclassing*: Only classes within the same file can extend and implement a sealed class.
- *Exhaustive type checking*: When using sealed class in `switch` statements or pattern matching, dart can ensure that all possible subclasses are handled.
- *Enhanced code safety*: Sealed classes make it easier to reason about the code and handle all possible classes, reducing errors.

```
sealed class NetworkState {}

class Loading extends NetworkState {}

class Success extends NetworkState {
  final String data;
  Success(this.data);
}

class Error extends NetworkState {
  final String message;
  Error(this.message);
}

void handleNetworkState(NetworkState state) {
  switch (state) {
    case Loading():
      print("Loading data...");
      break;
    case Success(:var data):
      print("Data loaded successfully: $data");
      break;
    case Error(:var message):
      print("Failed to load data: $message");
      break;
  }
}

void main() {
  handleNetworkState(Loading());              // Output: Loading data...
  handleNetworkState(Success("Sample Data")); // Output: Data loaded successfully: Sample Data
  handleNetworkState(Error("Network error")); // Output: Failed to load data: Network error
}
```

`When to Use Sealed Classes`
-  *Finite State Modeling*: When you have a limited set of well-defined states or types (e.g., state management, command patterns).
- *Exhaustive Pattern Matching*: When you want to leverage Dart’s type system to ensure all cases are handled.
- *Restricting Subclassing*: When you want to prevent external classes from extending or implementing a base class outside its defining file.

**Mixin**
	In dart, mixins are a way of reusing code across multiple classes. Mixins allow us to share methods and properties among different classes without using traditional inheritance. Instead of extending a base class, we can mix in a set of reusable methods or properties, giving classes additional functionality in a flexible way. Three keywords are used while mixins: `mixin`, `with`, `on`.

`Syntax`
```
mixin MixinName {
  // Methods and properties
}
```

`Key points`
- *Code reuse*: `Mixins` allow us to share functionality across multiple classes without forming a strict inheritance hierarchy.
- *No instantiation*: `Mixins` can not be instantiated directly. They are intended to be added to other classes.
- *With keyword*: `with` keyword is used to apply a `mixin` to a class.
- *No construction*: `Mixins` cannot have constructors because of `mixins` are meant to be `mixed into` existing classes rather than being instantiated on their own.
- *Flexible composition*: Multiple `mixins` can be applied to a single class, providing a form of multiple inheritance.

`Example`
```
mixin Musical {
  String instrument = "Piano";

  void play() {
    print("Playing the $instrument");
  }
}

class Musician with Musical {}

void main() {
  var musician = Musician();
  musician.play(); // Output: Playing the Piano
}
```

`Example of on keyword`
```
class Animal {
  void breathe() {
    print("Breathing...");
  }
}

mixin Swimmer on Animal {
  void swim() {
    breathe();
    print("Swimming in water");
  }
}

class Fish extends Animal with Swimmer {}

void main() {
  var fish = Fish();
  fish.swim(); // Output: Breathing... Swimming in water
}
```

`Difference between mixins, inheritance, and interface`

| Feature          | Mixins                  | Inheritance                           | Interfaces                  |
| ---------------- | ----------------------- | ------------------------------------- | --------------------------- |
| *Purpose*        | Code reuse              | Establishes a base class              | Defines a contract          |
| *Keyword*        | `with`                  | `extends`                             | `implements`                |
| *Instantiation*  | Cannot be instantiated  | Can be instantiated (if not abstract) | Cannot be instantiated      |
| *Multiple Usage* | Multiple mixins allowed | Single base class                     | Multiple interfaces allowed |
| *Constructor*    | No constructors allowed | Can have constructors                 | No constructors             |
`What is on and with keywords in mixins?`
*with*
The `with` keyword is used to *apply a mixin* to a class. It allows us to add methods and properties from the mixin to the class, enabling code reuse without using inheritance.

*on*
The `on` keyword is used in mixin declarations to *restrict the types of classes* that the mixin can be applied to. This is helpful when the mixin depends on methods or properties from a specific superclass.

**Difference Between `with` and `on` Keywords**

| Keyword | Purpose                                   | Usage                          |
| ------- | ----------------------------------------- | ------------------------------ |
| `with`  | Applies a mixin to a class                | `class Duck with Swimmable {}` |
| `on`    | Restricts mixin usage to specific classes | `mixin Swimmable on Animal {}` |
