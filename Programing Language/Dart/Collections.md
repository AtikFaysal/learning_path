**List**
> A `List` is an ordered collections of items that can contain duplicates, and can access item in a list by their index, and list can be either fixed-length or growable.

`Example`
```
void listPlayground(){  
  List<int> numbers = [10,20,30,40];  
  numbers.addAll([10,20,30,]);  
  print(numbers);  
  numbers.remove(10);//remove 10  
  print(numbers);  
  print(numbers.reversed);//print reversed  
  print(numbers.first);//print first item  
  
  numbers.insertAll(1, [500,1000]);//insert a list at index of 1  
  numbers.insert(0,100);//insert an item at index of 0  
  print(numbers);  
  
  numbers = Iterable<int>.generate(15).toList();//generate a list upto given limit  
  print(numbers);  
  
  var emptyList = [];  
  emptyList.add(10);//add an integer  
  emptyList.add('Atik');//add a string  
  emptyList.add(10.7);//add a decimal number  
  print(emptyList);  
  
  var fixedSizeList = List.filled(5, 10);//create a fixed size list with initial value  
  fixedSizeList[0] = 100;//update a value  
  print(fixedSizeList);  
  
  var isItemContains = fixedSizeList.contains(100);//check given item is contains or not  
  print(isItemContains);  
}
```

**Sets**
> A `set` in dart is an unordered collection of unique items, it's does not allow duplicate values. Sets are useful when we need to store a collection of item without duplicates.

`Example`
```
void setsPlayground(){  
  var number = {10,20,30,40};//create a new set  
  number.add(10);//add an item [duplicate item will be ignored]  
  print(number);  
  
  var anotherNumber = {30,50,9,90};  
  var uniqueItems = number.union(anotherNumber);//sets of unique item between two list  
  var intersectionItems = number.intersection(anotherNumber);//sets of common item between two list  
  print(uniqueItems);  
  print(intersectionItems);  
  
  var names = <String>{};//create a set of string items  
  names.add("Atik");//add an item  
  names.addAll({"Atik", "Faysal"});//add list of item  
  print(names);  
  
  final constantSet = const{  
    "A",  
    "B",  
    "C",  
    "D"  
  };  
  //constantSet[0] = "E";//this line will cause an error
  print(constantSet);  
}
```

**Map**
>A `Map` in Dart is a collection of key-value pairs, where each key is unique, and it associates to a value. Maps are also known as dictionaries or hash maps in other languages.

```
void mapPlayground(){  
  var gifts = {  
    // Key:    Value  
    'first': 'partridge',  
    'second': 'turtledoves',  
    'fifth': 'golden rings'  
  };//create a new map  
  
  var nobleGases = {  
    2: 'helium',  
    10: 'neon',  
    18: 'argon',  
  };//create a new map  
  
  var names = Map<int, String>();//create an empty map  
  names[0] = "A";  
  names[1] = "B";  
  names[2] = "C";  
  
  print(names);  
  print(gifts);  
  print(nobleGases);  
}
```

**Where**
>You can use where in list, set, map to **filter specific items**. It returns a new list containing all the elements that satisfy the condition. This is also called **Where Filter** in dart. Let’s see the syntax below

`Syntax`
```
Iterable<E> where(
bool test(
E element
)
)
```

`Example`
```
void wherePlayground(){  
  List<int> numbers = [10,20,30,40, 45,47,55,53];  
  var evenNumber = numbers.where((number)=> number % 2 == 0);  
  var oddNumber = numbers.where((number)=> number % 2 != 0);  
  print(evenNumber);  
  print(oddNumber);  
}
```
