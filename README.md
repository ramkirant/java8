# Functional Programming
### What is Functional Programming
Functional programming introduced in Java 8 aims to reduce the gap between business logic and the code. In functional programming, instead of saying how you want things to be done, we will say what we want to be done. In Functional programming, we pass functions as arguments and we use functions as statements. 

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
       .forEach(System.out::println)

