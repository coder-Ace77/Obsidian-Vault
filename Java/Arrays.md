
---

1. Arrays from java.lang.Object.
2. Arrays of reference types (`String[]`, `Object[]`) also implement Cloneable and Serializable interfaces.


> [!NOTE] Clonable and Serializable
> Marks a class as **serializable**, meaning its **objects can be converted into a byte stream**, which is useful for: 1.Saving to disk
> 2.Sending over a network   
>  3.Deep copying
>  
	>It’s a **marker interface** — it has **no methods**. It just tells the JVM: "This class can be serialized."
>
>Marks a class as **cloneable**, allowing its objects to be **duplicated** (deep or shallow copy).
>- You must **override** the `clone()` method from `Object`.
>- The class must **implement `Cloneable`** — otherwise, `clone()` throws `CloneNotSupportedException`.

#### Creating arrays:

Arrays of Primitive types and wrapper classes are easy to make.

```java
int[] numbers = new int[5];  // default: [0, 0, 0, 0, 0]
numbers[0] = 10;
numbers[1] = 20;

int[] arr = {1, 2, 3, 4, 5};  // Direct initialization

String[] names = new String[3];
names[0] = "Alice";
names[1] = "Bob";

String[] fruits = {"Apple", "Mango", "Banana"};

// we can create arrays of dynamic size
int n = 5; // can be taken from user input
String[] arr = new String[n]; // creaating string of size n
```

1. Java arrays have field name length.
2. Arrays are of constant sizes.
3. Arrays of custom object default to `null`
4. Arrays are stored in **heap memory**
5. The variable holds a reference to the memory block.

Storing custom objects

```java
class Student {
    String name;
    Student(String name) { this.name = name; }
}

Student[] students = new Student[2];
students[0] = new Student("Adil");
students[1] = new Student("Sara");
```

Higher order arrays:

```java
int[][] matrix = new int[3][4];  // 3 rows, 4 columns

matrix[0][0] = 1;
matrix[1][2] = 5;

Student[][] seats = new Student[2][2];
seats[0][0] = new Student("Adil");

```

Jagged arrays:

These are 2d arrays with vaible column sizes;

```java
int[][] jagged = new int[3][];
jagged[0] = new int[2];  // 2 elements in row 0
jagged[1] = new int[1];  // 1 element in row 1
jagged[2] = new int[3];  // 3 elements in row 2
```


### Array methods:

```java
import java.util.Arrays;
```

Sorting
```java
int[] arr = {3, 1, 2};
Arrays.sort(arr);  // arr becomes [1, 2, 3]
```

Converting to string

```java
Arrays.toString()
```

Arrays.copyOf
```java
int[] original = {1, 2, 3};
int[] copy = Arrays.copyOf(original, 5);  // [1, 2, 3, 0, 0]
```

Arrays.fill
```java
int[] arr = new int[5];
Arrays.fill(arr, 42);  // [42, 42, 42, 42, 42]
```

Array to List
```java
String[] arr = {"A", "B", "C"};
List<String> list = Arrays.asList(arr);
```



---

### Java stream operations

**Streams** in Java provide a **declarative** and **functional-style** approach to process **collections or arrays**. They allow you to **filter**, **map**, **reduce**, **sort**, and **collect** data with minimal code.

A **stream** is a sequence of elements that supports **pipeline operations** (like map, filter, reduce) to process data.
> Streams **do not store data** — they just process it.

#### Stream from Arrays

```java
import java.util.stream.*;
int[] arr = {1, 2, 3, 4, 5};
// Convert to IntStream (primitive stream)
IntStream stream = Arrays.stream(arr);
```

```java
String[] names = {"Alice", "Bob", "Charlie"};
Stream<String> nameStream = Arrays.stream(names);
```

Stream operations can be of two types:

1. Terminal operations: They return a new stream.
eg: map() , filter()
2. Intermediate operations: Produces a result and ends the stream. 
eg: forEach() , sum()

| Task               | Code Example                     |
| ------------------ | -------------------------------- |
| Sum                | `stream.sum()`                   |
| Average            | `stream.average().getAsDouble()` |
| Map (e.g., square) | `map(x -> x * x)`                |
| Filter even        | `filter(x -> x % 2 == 0)`        |
| Count condition    | `filter(...).count()`            |
| Max/Min            | `max().getAsInt()`               |
| Collect to List    | `collect(Collectors.toList())`   |
| Sort               | `sorted()`                       |

examples:

```java
int[] arr = {1, 2, 3, 4, 5};
int sum = Arrays.stream(arr).sum();   // 15

Arrays.stream(arr)
      .map(x -> x * x)
      .forEach(System.out::println);

Arrays.stream(arr)
      .filter(x -> x % 2 == 0)
      .forEach(System.out::println);  // prints 2, 4

int max = Arrays.stream(arr).max().getAsInt();
int min = Arrays.stream(arr).min().getAsInt();

String[] names = {"Alice", "Bob", "Charlie"};

List<String> list = Arrays.stream(names)
                          .filter(name -> name.startsWith("A"))
                          .collect(Collectors.toList());
```

#### Passing arrays

In Java, arrays are **passed by reference**, meaning when you pass an array to a method, you're passing the **reference (memory address)** to that array — not a copy.

```java
returnType methodName(dataType[] arrayName)
```

#### For loops

In Java, arrays are often used with **loops** to access, modify, or print their elements. The most common types of loops used with arrays are:

```java
int[] arr = {10, 20, 30, 40};

for (int i = 0; i < arr.length; i++) {
    System.out.println("Index " + i + ": " + arr[i]);
}
```

for Each loop

```java
for (int num : arr) {
    System.out.println(num);
}

// for each with 2d array
for (int[] row : matrix) {
    for (int val : row) {
        System.out.print(val + " ");
    }
    System.out.println();
}
```

