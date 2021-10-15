# Functional Programming
### What is Functional Programming
Functional programming introduced in Java 8 aims to reduce the gap between business logic and the code. In functional programming, instead of saying how you want things to be done, we will say what we want to be done. In Functional programming, we pass functions as arguments and we use functions as statements. 

### What is Lambda Expression
Lambda expression is a simplified representation of a method. 

### What is a method reference
Method reference is a way, using which, in Java 8, we convert a method into an expression. Using method references, we can pass a method as an argument to a function. 

### Streams
Operations that can be performed on streams can be categorized into two categories
#### Intermediate operations
Intermediate operations are the operations that are performed on a stream and they return a stream. Operations including filter, map, sorted, distinct fall into the Intermediate operations category. Intermediate operations return a stream.

#### Terminal operations
Terminal operations are the last operations that we perform on a stream. Terminal operations do not return a stream but they return a specific type. Operations including forEach, collect, reduce fall into the Terminal operations category. 

### Convert a list to a stream
```java
Stream<Integer> integerStream = numbers.stream();
```

### Iterating a stream
We iterate a stream by using the forEach method and passing a method reference to it. We reference a method by using the syntax. **Class::function**. We can only pass static methods in method references.
```java
numbers.stream()
       .forEach(System.out::println);
```

### Filtering a stream
```java
numbers.stream()
       .filter(i -> i%2 == 0)
       .forEach(System.out::println);
```

### Aggregating a stream into a single value
We can aggregate a stream into a single value (like sum of all numbers) by using the **reduce** method.
```java
numbers.stream()
       .reduce(0, (x,y)->x+y);
```
Here 0 is the initial value. Stream passes 0 and first value to x, y. The sum and next value is again passed to x, y.

Another way of reducing is by using the core class methods.
```java
numbers.stream()
       .reduce(0, Integer::sum);
```

### Getting the distinct values from the stream
```java
numbers.stream()
       .distinct()
       .forEach(System.out::println);
```
### Sort the values from the stream
```java
numbers.stream()
       .sorted()
       .forEach(System.out::println);
```
#### Sort in ascending order
```java
numbers.stream()
       .sorted(Comparator.naturalOrder())
       .forEach(System.out::println);
```
#### Sort in descending order
```java
numbers.stream()
       .sorted(Comparator.reverseOrder())
       .forEach(System.out::println);
```
#### Custom sorting (Sort with the length of the string)
```java
numbers.stream()
      .sorted(Comparator.comparing(str -> str.length()))
      .forEach(System.out::println);
```
### Collect the output of a stream
#### Collect to a list
```java
List<Integer> doubleList = numbers.stream()
                                  .map(number -> number*number)
                                  .collect(Collectors.toList());
```
### Functional Interfaces
An interface having exactly one abstract method annotated with **@FunctionalInterface** annotation is a functional interface. Functional interfaces can have default or static methods. There are three types of functional Interfaces
#### Predicate
A Predicate has a single public method **test**. Example of a predicate
```java
x -> x%2==0

/* Internally, compiler converts the above expression something like below*/
Predicate<Integer> eventPredicate = new Predicate<Integer>(){
       @Override
       public boolean test(Integer x) {
              return x%2 == 0;
       }
}
```
#### Function
Function accepts one argument and produces a result. A function has a single public method called **apply**. Example of a function
```java
x -> x*x

/*Internally, compiler converts the above expression something like below*/
Function<Integer, Integer> squareFunction = new Function<Integer, Integer>() {
       @Override
       public Integer apply(Integer x) {
              return x*x;
       }
}
```

### Binary Operator
Binary Operator takes two arguments and produces a single result. Binary operator has a single public method called **apply**. Example of a Binary Operator
```java
(x,y) -> x+y

/*Internally, compiler converts the aboe expression something like below*/
BinaryOperator<Integer> binaryOperator = new BinaryOperator<Integer>() {
       @Override
       public Integer apply(Integer x, Integer y) {
              return x+y;
       }
}
```
#### Consumer
Represents an operation that accepts a single argument and returns no result. A consumer has a single public method called **accept**. Example of a Consumer
```java
System.out::println

/*Internally, compiler converts the above expression something like below*/
Consumer<Integer> sysOutConsumer = new Consumer<Integer>() {
       @Override
       public void accept(Integer x) {
              System.out.println(x);
       }
}
```
