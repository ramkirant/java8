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

### Match Predicates
#### allMatch
allMatch returns true if all the elements of the stream satisfies the predicate condition. It will return false even if a single element dont satisfy the condition.
```java
courses.stream().allMatch(course -> course.getReviewScore() > 90)
```
#### anyMatch
anyMatch returns true if atleast one element of the stream satisfies the predicate condition. It will return false only if all the elements dont satisfy the condition.
```java
courses.stream().anyMatch(course -> course.getReviewScore() > 90)
```
#### noneMatch
noneMatch returns true if none of the element of the stream satisfies the predicate condition. It will return false if all the elements satisfies the condition.
```java
courses.stream().noneMatch(course -> course.getReviewScore() > 90)
```
### skip and limit
If we want to pick up only the first x number of elements from the stream, we can use **limit**.
```java
Comparator<Course> comparingByNoOfStudentsAndNoOfReviews = Comparator.comparingInt(Course::getNoOfStudents).thenComparingInt(Course::getNoOfReviews);
List<Course> first5List = courses.stream()
                                 .sorted(comparingByNoOfStudentsAndNoOfReviews)
				 .limit(5)
				 .collect(Collectors.toList());
```
If we want to skip the first x number of elements from the stream, we can use **skip**
```java
Comparator<Course> comparingByNoOfStudentsAndNoOfReviews = Comparator.comparingInt(Course::getNoOfStudents).thenComparingInt(Course::getNoOfReviews);
List<Course> skip5List = courses.stream()
                                .sorted(comparingByNoOfStudentsAndNoOfReviews)
				.skip(5)
				.collect(Collectors.toList());
```

### takeWhile and dropWhile
We can use **takeWhile** to collect all the elements till the predicate condition is not satisfied.
```java
Comparator<Course> comparingByNoOfStudents = Comparator.comparingInt(Course::getNoOfStudents);
List<Course> allCoursesUpto95Students = courses.stream()
                                               .sorted(comparingByNoOfStudents)
					       .takeWhile(course -> course.getReviewScore() >= 95)
					       .collect(Collectors.toList());
```
We can use **dropWhile** to drop all the elements till the predicate condition is not satisfied.
```java
Comparator<Course> comparingByNoOfStudents = Comparator.comparingInt(Course::getNoOfStudents);
List<Course> dropCoursesUpto95Students = courses.stream()
                                               .sorted(comparingByNoOfStudents)
					       .dropWhile(course -> course.getReviewScore() >= 95)
					       .collect(Collectors.toList());
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

#### Custom sorting of objects
```java
Comparator<Course> comparingByNoOfStudentsIncreasing = Comparator.comparing(Course::getNoOfStudents);
courses.stream().sorted(comparingByNoOfStudentsIncreasing).forEach(System.out::println);
Comparator<Course> comparingByNoOfStudentsDecreasing = Comparator.comparing(Course::getNoOfStudents).reversed();
courses.stream().sorted(comparingByNoOfStudentsDecreasing).forEach(System.out::println);
Comparator<Course> comparingByNoOfStudentsAndNoOfReviews = Comparator.comparing(Course::getNoOfStudents).thenComparing(Course::getNoOfReviews);
courses.stream().sorted(comparingByNoOfStudentsAndNoOfReviews);
```
Also, we can use the primitive specific comparing like **comparingInt** and **thenComparingInt** for more efficient operations if we are comparing primitive types
```java
Comparator<Course> comparingByNoOfStudentsIncreasing = Comparator.comparingInt(Course::getNoOfStudents);
courses.stream().sorted(comparingByNoOfStudentsIncreasing).forEach(System.out::println);
Comparator<Course> comparingByNoOfStudentsDecreasing = Comparator.comparingInt(Course::getNoOfStudents).reversed();
courses.stream().sorted(comparingByNoOfStudentsDecreasing).forEach(System.out::println);
Comparator<Course> comparingByNoOfStudentsAndNoOfReviews = Comparator.comparingInt(Course::getNoOfStudents).thenComparingInt(Course::getNoOfReviews);
courses.stream().sorted(comparingByNoOfStudentsAndNoOfReviews);
```

### Collect the output of a stream
#### Collect to a list
```java
List<Integer> doubleList = numbers.stream()
                                  .map(number -> number*number)
                                  .collect(Collectors.toList());
```
### Functional Interfaces
An interface having exactly one abstract method annotated with **@FunctionalInterface** annotation is a functional interface. This abstract method is called as function descriptor. Functional interfaces can have default or static methods. There are three types of functional Interfaces
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
Function accepts one argument and produces a result. A function has a single abstract method called **apply**. Example of a function
```java
x -> x*x

/*Internally, compiler converts the above expression something like below. Here, Function is like Function<InputDatatype, OutputDatatype>*/
Function<Integer, Integer> squareFunction = new Function<Integer, Integer>() {
       @Override
       public Integer apply(Integer x) {
              return x*x;
       }
}
```

### Unary Operator
Unary Operator takes a single argument and produces a single result. For Unary Operator, input and output should be of the same datatype. Unary operator has a single abstract method called **apply**.  Example of a Unary Operator
```java
(x) -> 3 * x;
```

### Binary Operator
Binary Operator takes two arguments and produces a single result. For Binary Operator, input and output should be of the same datatype. Binary operator has a single abstract method called **apply**. Example of a Binary Operator
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
Represents an operation that accepts a single input and returns no output. A consumer has a single absract method called **accept**. Example of a Consumer
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

### Supplier
Supplier is the opposite of Consumer. Supplier dont accept any input but returns an output. A supplier has a single abstract method called **get**. Exmple of a supplier
```java
() -> {
	Random random = new Random();
	return random.nextInt(1000);
}
```

### BiPredicate
BiPredicate, takes two inputs and returns a **boolean** as an output. Function Descriptor for BiPredicate is **test**
```java
BiPredicate<Integer, String> biPredicate = (number, str) -> {
	return number<10 && str.length()>5
}
System.out.println(biPredicate.test(15, "TestingString"));
```

### BiFunction
BiFunction takes two inputs and returns a single output. Function Descriptor for BiFunction is **apply**.
```java
BiFunction<Integer, String, String> biFunction = (number, str) -> number+ " "+str;
System.out.println(biFunction.apply(15, "TestingString"));
```

### BiConsumer
BiConsumer takes two inputs and consumes it. Function Descriptor for BiConsumer is **accept**.
```java
BiConsumer<String, String> biConsumer = (s1, s2) -> {
	System.out.println(s1+" "+s2) 
};
biConsumer.accept();
```

### Summary of Functional Interfaces
| Interface | Lambda Expression | Function Descriptor |
| --------- | ----------------- | ------------------- |
| Predicate | x -> x%2=0        | test |
| BiPredicate | (x,y) -> x%y=0 | test |
| Function  | x -> x * x        | apply |
| BiFunction | (x,y) -> x+y | apply
| Unary Operator | (x) -> 3 * x | apply |
| Binary Operator | (x,y) -> x+y | apply |
| Consumer | System.out::println | accept |
| BiConsumer | (x,y) -> System.out.println(x+ " " + y)| accept |
| Supplier | () -> 5 | get | 



### Behavior parameterization with Functional programming
With Behavior parameterization, we can pass the logic / algorithm as an argument to a function. Refer to the below example on how to do Behavior parameterization
```java
public class FP03BehaviorParameterization {
	public static void main(String[] args) {
		List<Integer> numbers = List.of(4,6,8,1,3,5,5,7,1,2,9,2,4);
		
		filterAndPrint(numbers, x -> x%2==0);
		
		filterAndPrint(numbers, x -> x%2!=0);
	}

	private static void filterAndPrint(List<Integer> numbers, Predicate<Integer> predicate) {
		numbers.stream()
			   .filter(predicate)
			   .forEach(System.out::println);
	}
}
```

### Type inference of lambda expressions
We an declare a type when defining a lambda expression. When we declare a type, we need to declare the type for all the variables of lambda expression. We can declare the type as below
```java
Predicate<Integer> isEvenPredicate = (Integer x) -> x % 2 == 0  
```

### Method References in lambda expressions
```java
courses.stream()
       .map(str -> str.toUpperCase())
       .forEach(System.out::println)
```
Can be replaced with
```java
courses.stream()
       .map(String::toUpperCase)
       .forEach(System.out::println)
```

```java
Supplier<String> supplier = () -> new String() 
```
Can be replace with
```java
Supplier<String> supplier = String::new
```
