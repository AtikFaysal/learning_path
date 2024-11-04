**Basic operators**
`Arithmetic operators`
- `+` (Addition): `a + b`
- `-` (Subtraction): `a - b`
- `*` (Multiplication): `a * b`
- `/` (Division): `a / b` (returns a `double`)
- `~/` (Integer Division): `a ~/ b` (returns an `int`)
- `%` (Modulus): `a % b` (remainder of division)

`Example`
```
void main() {
  int a = 10;
  int b = 3;
  print(a + b);  // 13
  print(a - b);  // 7
  print(a * b);  // 30
  print(a / b);  // 3.3333333333333335
  print(a ~/ b); // 3
  print(a % b);  // 1
}
```

`Relational operators`
- `==` (Equal to)
- `!=` (Not equal to)
- `>` (Greater than)
- `<` (Less than)
- `>=` (Greater than or equal to)
- `<=` (Less than or equal to)

`Example`
```
void main() {
  int x = 5;
  int y = 10;
  print(x == y);  // false
  print(x != y);  // true
  print(x > y);   // false
  print(x < y);   // true
  print(x >= y);  // false
  print(x <= y);  // true
}
```

`Logical operators`
- `&&` (Logical AND): true if both conditions are true
- `||` (Logical OR): true if at least one condition is true
- `!` (Logical NOT): inverts the value of a condition

`Example`
```
void main() {
  bool isSunny = true;
  bool isWarm = false;
  print(isSunny && isWarm); // false
  print(isSunny || isWarm); // true
  print(!isSunny);          // false
}
```

`Increment & decrement operators`
- `++var` pre increment 
- `--var` pre decrement
- `var++` post increment
- `var--` post decrement

`Example`
```
void main() {
	// declaring two numbers 
	 int num1=0;
	 int num2=0;
	 
	// performing increment / decrement operator  
	
	// pre increment   
	num2 = ++num1;
	print("The value of num2 is $num2");
	
	// reset value to 0 
	num1 = 0;
	num2 = 0;
	
	// post increment  
	num2 =  num1++;
	print("The value of num2 is $num2");  
}
```

`Assignment operators`
- `=` (Simple assignment): `a = b`
- `+=`, `-=`, `*=`, `/=`, `%=` (Compound assignments): `a += b` is equivalent to `a = a + b`

`Example`
```
void main() {
  int a = 5;
  a += 3;  // a = a + 3
  print(a); // 8
}
```

**Control flow operators**
`if-else statement`
```
void main() {
  int age = 20;
  if (age >= 18) {
    print("Adult");
  } else if(age >= 10){
    print("Minor");
  }else {
	print("Child")
  }
}
```

`Ternary operator`
```
void main() {
  var number = 11;
  var oddOrEven = (number % 2 == 0) ? "Even" : "Odd"; 
  print(oddOrEven);
}
```

`For loop`
```
void main() {
  var numbers = [1, 2, 3, 4];
  for (var num in numbers) {
    print(num);
  }
}
```

`For each loop`
```
void main() {
  List<String> fruits = ['apple', 'banana', 'cherry'];

  fruits.forEach((fruit) {
    print(fruit);
  });

 //single line statement
  fruits.forEach( (fruit)=>print(fruit));
}
```

`For In loop`
```
void main() {
  List<String> fruits = ['apple', 'banana', 'cherry'];
  
  for(String fruit in fruits){
    print(fruit);
  }
}
```

`while loop`
```
void main() {
  int count = 0;
  while (count < 5) {
    print(count);
    count++;
  }
}
```

`Switch statement`
```
void main() {
  String grade = 'A';
  switch (grade) {
    case 'A':
      print("Excellent");
      break;
    case 'B':
      print("Good");
      break;
    case 'C':
      print("Average");
      break;
    default:
      print("Grade not recognized");
  }
}
```

`break and continue statement`
```
void main() {
  for (int i = 0; i < 5; i++) {
    if (i == 3) {
      break;  // Exits the loop when i is 3
    }
    print(i);
  }

  for (int i = 0; i < 5; i++) {
    if (i == 2) {
      continue;  // Skips the iteration when i is 2
    }
    print(i);
  }
}
```

**Exceptional handling**
`Syntax`
```
try {
// Your Code Here
}
catch(ex){
// Exception here
}
```

`Example`
```
void main() {   
   int a = 18;   
   int b = 0;   
   int res;    
     
   try {    
      res = a ~/ b;
      print("Result is $res");   
   }    
    // It returns the built-in exception related to the occurring exception  
   catch(ex) {   
      print(ex);   
    }   
}  
```
