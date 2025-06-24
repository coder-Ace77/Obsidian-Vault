
---

**Functional Programming (FP)** is a paradigm where computation is treated as the evaluation of mathematical functions without changing state or mutable data. Java began supporting functional programming concepts robustly in **Java 8** with the introduction of **lambdas**, **streams**, and **functional interfaces**.

#### Lambdas

```java
Function<Integer, Integer> square = x -> x * x;
System.out.println(square.apply(5)); // 25
```


Interfaces with a **single abstract method** (SAM). Common examples:

| Interface        | Purpose                    |
| ---------------- | -------------------------- |
| `Function<T, R>` | Takes `T`, returns `R`     |
| `Predicate<T>`   | Takes `T`, returns boolean |
| `Consumer<T>`    | Takes `T`, returns nothing |
| `Supplier<T>`    | Takes nothing, returns `T` |
Secondly we excessively use STREAMS api Enables functional-style operations on collections (map, filter, reduce). 

```java
List<String> names = List.of("Alice", "Bob", "Charlie");
List<String> filtered = names.stream()
    .filter(name -> name.length() > 3)
    .map(String::toUpperCase)
    .collect(Collectors.toList());
System.out.println(filtered); // [ALICE, CHARLIE]
```

Why functional programming?

1. In FP, data is immutable by default, meaning values don't change after they're created. This eliminates a whole class of bugs caused by **shared mutable state**, race conditions, or unexpected side effects. For example, a function that calculates a result from an input doesn’t modify any global variable—it just returns a new result.
2. A _pure function_ always produces the same output for the same input and has no side effects (like modifying files or changing global variables). This makes functions **predictable**, **easier to test**, and easier to reason about in isolation. You don’t need to track complex state transitions or dependencies while debugging.
3. Functional programming is assignment less programming meaning me will not use = anywhere this eleminates any kind of side effect.
4. Functions now are considered first class citizen. Any first class citizen can be moved around and thrown around. Passed as arg and can be returned. 
5. Higher Function can pass function and also return function.
6. Functions have to be pure.
	1. Pure functions don't have side effect. It does not change anything. 
	2. Pure function does not depend upon anything that changes as well.
7. This means data will not be changed. You have create new objects to create new data.
8. Secondly outside can not change the data. Becasue we want out functional programming to be lazy and so nothing outside must change the internal code.
9. We introduce state transformation instead of state mutation.

Lambda function have just param list and body. Name is anonymous and return type is infereed from context.
(param)-> body

##### Internal Iterator:

```java
List<Integer> numbers = Arrays.asList(1,2,3);
// what to do not how to do
numbers.forEach((Integer e)->System.out.println(e));
numbers.forEach((e)->System.out.println(e)); // type can infered at compile time
numbers.forEach(System.out::println); // method reference will auto apply on each element
```

```java
// gettting the sum of even numbers
System.out.println(numbers.stream().filter(e->e%2==0).map(e->e*2).sum());
```


### Reactive programming in java

**Reactive Programming** is an **asynchronous, non-blocking programming paradigm** focused on handling **streams of data** and **reacting to changes or events** over time. It’s ideal for applications that require high responsiveness, scalability, and efficient use of system resources—such as real-time apps, APIs, and microservices.

- You are building **I/O-bound** or **event-driven** applications
- You need **high-throughput**, **low-latency** systems (e.g., chat apps, APIs)
- You want to **compose async pipelines** of data transformations


