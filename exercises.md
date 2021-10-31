### jshell
jshell comes as a command line utility with java 9. If java 9 is installed, we can invoke jshell by typing **jshell** in terminal or command prompt. If we dont have java 9 installed, we can invoke jshell using https://tryjshell.org

### Exercise 1
Print only odd numbers from the list
```java
List<Integer> numbers = List.of(4,6,8,1,3,5,5,7,1,2,9,2,4);
```

### Exercise 2
Print all courses individually
```java
List<String> courses = List.of("Java", "Golang", "Kubernetes", "Spring", "Spring Boot");
```

### Exercise 3
Print courses containing the word Spring

### Exercise 4
Print courses whose name has atleast 4 letters

### Exercise 5
Print the cubes of odd numbers

### Exercise 6
Print the number of characters in each course name

### Exercise 7
Square every number in a list and find the sum of squares

### Exercise 8
Cube every number in the list and find the sum of cubes

### Exercise 9
Find the sum of odd numbers in the list

### Exercise 10
Sort the numbers in ascending order

### Exercise 11
Sort the numbers in descending order

### Exercise 12
Sort the courses in the length of their name

### Exercise 13
Square the numbers and collect the output to a list

### Exercise 14
Create a list with the length of all course titles. 

### Exercise 15
Return true if all the numbers are even. Else return false

### Exercise 16
Return true if atleast one number is even. Else return false

### Exercise 17
Return true if none of the number is even. Else return false

### Exercise 18
Find the functional interface behind the second argument of the reduce method. Create an implementation for the Functional interface
```java
int sum = numbers.stream().reduce(0, Integer::sum)
```
### Exercise 19
Do Behavior parameterization for the below mapping logic
```java
List squaredNumbers = numbers.stream().map(x -> x * x).collect(Collectors.toList())
```

### Will the below compile?
1. Consumer<String> consumer = () -> {}
2. Consumer<String> consumer = System.out::println
3. Consumer<String> consumer = (str) -> System.out.println(str)
4. BiConsumer<String, String> biConsumer = (str1, str2) -> System.out.println(str1)
5. Supplier<String> supplier = () -> "Ram"
6. Supplier<String> supplier = () -> {"Ram";}
7. Suplier<String> supplier = () -> {return "Ram";}
8. Consumer<String> consumer = (str) -> System.out.println(str); System.out.println(str);

