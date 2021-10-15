# Functional Programming
### What is Functional Programming
Functional programming introduced in Java 8 aims to reduce the gap between business logic and the code. In functional programming, instead of saying how you want things to be done, we will say what we want to be done. In Functional programming, we pass functions as arguments and we use functions as statements. 

### What is Lambda Expression
Lambda expression is a simplified representation of a method. 

### What is a method reference
Method reference is a way, using which, in Java 8, we convert a method into an expression. Using method references, we can pass a method as an argument to a function. 

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
