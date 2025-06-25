
---

![[Pasted image 20250620093137.png]]

### Stack

LIFO structure.

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
```

common methods:

|Method|Description|
|---|---|
|`push(E item)`|Pushes an item onto the top of the stack|
|`pop()`|Removes and returns the top item|
|`peek()`|Returns the top item without removing it|
|`isEmpty()`|Returns `true` if the stack is empty|
|`size()`|Returns the number of elements in the stack|
|`search(Object o)`|Returns 1-based position from top of stack or -1 if not found|
Note that poll is the operation used in reference with queue like data structure.

### Queue

Queue is just an interface with concrete implementation as LinkedList or ArrayDeque.
Moslty used however is LinkedList.

```java
import java.util.Queue;
import java.util.LinkedList;

Queue<Integer> queue = new LinkedList<>();
```

Common Methods:

|Method|Description|
|---|---|
|`add(E e)`|Adds element to the rear (throws exception if fails)|
|`offer(E e)`|Adds element to the rear (returns `false` if fails)|
|`remove()`|Removes and returns the front element (throws exception if empty)|
|`poll()`|Removes and returns the front element (`null` if empty)|
|`element()`|Returns front element without removing (throws exception if empty)|
|`peek()`|Returns front element without removing (`null` if empty)|
|`isEmpty()`|Checks if queue is empty|
|`size()`|Returns number of elements|
Although add and remove method persisit they should not be used because they give error when fail.
On the other hand poll() peek() and offer() return null when fail or return false.

But we should use these three operations:

peek()-> see the front element
poll() -> return and remove the front element
offer() -> add to end

### Priority queue:

It is direct implementation of heap in java.

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();
```

|Method|Description|
|---|---|
|`add(E e)`|Adds element to the queue|
|`offer(E e)`|Same as `add()`|
|`poll()`|Removes and returns the smallest element|
|`peek()`|Returns (but doesn't remove) the smallest element|
|`isEmpty()`|Checks if queue is empty|
|`size()`|Returns number of elements|
Again add exist but should not be used. we should use

offer()
poll()
peek() as our primary mathods.

Priority queue can also be created to handle custom ordering. 
Mainly there are two ways creating comparator or using lambda.

```java
class Pair {
    int value, priority;
    Pair(int v, int p) {
        value = v;
        priority = p;
    }
}

PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> a.priority - b.priority);
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
```

1. As discussed in lambda we can omit the datatype of params and java itself is capable enough to guess the datatype at compile time. 
2. Second in custom comparison only following rule is followed everywhere. 
	1. return -1 if first element of arg you want before second
	2. return 0 if both are equal
	3. return 1 if first one should come after second.

### Deque:

In java deque is an interface commonly implemented by ArrayDeque.

```java
import java.util.Deque;
import java.util.ArrayDeque;

Deque<Integer> deque = new ArrayDeque<>();
```

Common Methods:

|Method|Description|
|---|---|
|`addFirst(e)`|Insert at front|
|`addLast(e)`|Insert at rear|
|`removeFirst()`|Remove from front|
|`removeLast()`|Remove from rear|
|`peekFirst()`|View front without removing|
|`peekLast()`|View rear without removing|
|`offerFirst(e)`|Add at front (no exception if full)|
|`offerLast(e)`|Add at rear (no exception if full)|
|`pollFirst()`|Remove from front (null if empty)|
|`pollLast()`|Remove from rear (null if empty)|
|`isEmpty()`|Check if deque is empty|
|`size()`|Number of elements|
Again three main operations:

peek-> first or last -> peekFirst() / peekLast()
poll -> first or last -> peekFirst() / peekLast()
offer -> first or last -> offerFirst() / offerLast()

This ends our simple data structures linear ones.

### ArrayList

In Java, an **`ArrayList`** is a **resizable array** that is part of the `java.util` package.

```java
import java.util.ArrayList;
ArrayList<Integer> list = new ArrayList<>();

// with initial capacity
ArrayList<String> names = new ArrayList<>(100);
```

|Method|Description|
|---|---|
|`add(E e)`|Appends element to the end|
|`add(int index, E)`|Inserts element at a specific index|
|`get(int index)`|Returns element at index|
|`set(int index, E)`|Replaces element at index|
|`remove(int index)`|Removes element at index|
|`remove(Object o)`|Removes first occurrence of the element|
|`contains(Object o)`|Checks if element exists|
|`indexOf(Object o)`|Returns first index of element or -1|
|`size()`|Returns the number of elements|
|`clear()`|Removes all elements|
|`isEmpty()`|Checks if the list is empty|
main methods are `add()` commonly add to end `set()` to update values or `get()` to get value at index.
`reomve()` erases last element of array. 

contains() / indexOf() -> can be used to find if certain object is present or not.

##### Collections.nCopies:

This is really helpfull function which helps us to initialize the arraylist with given values.
However the list created will be immutable meaning all elements share a common internal object. So use manual loop.

```java
List<Integer> list = new ArrayList<>(Collections.nCopies(10,5)); // num , val
```

##### Filling an array:

Intialization through literals

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

int[][] jagged = {
    {1},
    {2, 3},
    {4, 5, 6}
};
```

We can use arrays.fill()

```java
Arrays.fill(arr, startIndex, endIndex, value);  // fills index 1 to 3 with 99
```

How to fill 2d arrays / arraylist -> using loops:

```java
int[][] grid = new int[3][4]; // 3 rows, 4 columns
// Fill with a value (e.g. 5)
for (int i = 0; i < 3; i++) {
    Arrays.fill(grid[i], 5);
}
```

```java
int rows = 3, cols = 4;
ArrayList<ArrayList<Integer>> matrix = new ArrayList<>();

for (int i = 0; i < rows; i++) {
    ArrayList<Integer> row = new ArrayList<>(Collections.nCopies(cols, 0));  // Fill row with 0s
    matrix.add(row);
}
```

Converting array to arraylist
```java
List<String> list = Arrays.asList(arr);  // Fixed-size list backed by the array usually used for stream operattons.

List<String> modifiableList = new ArrayList<>(Arrays.asList(arr)); // safe and modifiable
```

List to array:

```java
List<String> list = List.of("x", "y", "z");

String[] arr = list.toArray(new String[0]);
// You must pass a typed array for generic conversion.
```

### Strings

Strings in java are immutable and cannot be changed. All string operations like concat(), + etc create new objects. It is object of `Java.lang.String` class.
1. **Immutable**: Once created, it cannot be changed.
2. **Stored in String Pool** (in heap memory) for reuse.
3. **Stored in String Pool** (in heap memory) for reuse.

Creation if done from literals create string in string pool. However if used new keyword created new object.

```java
String s1 = "Java";
String s2 = "Java"; // points to the same object as s1
System.out.println(s1 == s2); // true

String s3 = new String("Java");
System.out.println(s1 == s3); // false
```

```java
String s = "Hello";
s += " World"; // Creates a new string internally
System.out.println(s);  // Hello World
```

| Method                             | Description                                    |
| ---------------------------------- | ---------------------------------------------- |
| `length()`                         | Returns the number of characters               |
| `charAt(index)`                    | Returns character at index                     |
| `substring(start, end)`            | Extracts part of the string                    |
| `equals(str)`                      | Checks if two strings are equal                |
| `equalsIgnoreCase(str)`            | Ignores case during comparison                 |
| `compareTo(str)`                   | Lexicographic comparison                       |
| `contains(str)`                    | Checks if string contains substring            |
| `indexOf(str)`                     | First occurrence index                         |
| `lastIndexOf(str)`                 | Last occurrence index                          |
| `toLowerCase()`, `toUpperCase()`   | Converts case                                  |
| `trim()`                           | Removes leading and trailing whitespaces       |
| `replace(a, b)`                    | Replaces all occurrences of a with b           |
| `split(regex)`                     | Splits string into array using regex delimiter |
| `startsWith(str)`, `endsWith(str)` | Checks string start/end                        |
There is also a type called `charArray` One can convert string to charArray

```java
String str = "hello";
char[] chars = str.toCharArray();
// now all opertions of array can be done on charArray. for ex reversing

String str1 = new String(chars); // char array to string
```

### String Builder

`StringBuilder` is a **mutable** sequence of characters — unlike `String`, which is **immutable**. It's part of `java.lang` and is used when you need to **modify strings frequently**, especially inside loops.

```java
StringBuilder sb = new StringBuilder();          // empty
StringBuilder sb2 = new StringBuilder("hello");  // initialized with "hello"
```

Constructors:

```java
StringBuilder()                     // default capacity (16)
StringBuilder(int capacity)         // with initial capacity
StringBuilder(String str)           // initialized with a string
```

Methods:

| Method                     | Description                                       |
| -------------------------- | ------------------------------------------------- |
| `append(x)`                | Adds to the end (supports any type)               |
| `insert(index, str)`       | Inserts at specified position                     |
| `delete(start, end)`       | Deletes from start (inclusive) to end (exclusive) |
| `deleteCharAt(index)`      | Deletes one character at index                    |
| `replace(start, end, str)` | Replaces part of string                           |
| `reverse()`                | Reverses the string                               |
| `charAt(index)`            | Returns character at index                        |
| `setCharAt(index, ch)`     | Modifies character at index                       |
| `toString()`               | Converts to String                                |
| `length()` / `capacity()`  | Current length or capacity                        |
| `ensureCapacity(n)`        | Ensures buffer capacity                           |
| `trimToSize()`             | Trims internal buffer to actual length            |
Observe that append() delete() charAt() , setCharAt() are most important 


```java
String s = "abc";
StringBuilder sb = new StringBuilder(s); // string to string builder

String result = sb.toString(); // Convert back to string
```

### HashMap:

```java
import java.util.HashMap;
HashMap<KeyType, ValueType> map = new HashMap<>();
```

Common methods:

|Method|Description|
|---|---|
|`put(k, v)`|Insert or update a value|
|`get(k)`|Returns value for key or null|
|`containsKey(k)`|Checks if key exists|
|`remove(k)`|Removes entry|
|`keySet()`|Returns a Set of keys|
|`values()`|Returns Collection of values|
|`entrySet()`|Returns Set of key-value pairs|

DSA use cases

| Problem Type     | Usage                                         |
| ---------------- | --------------------------------------------- |
| Frequency count  | `map.put(x, map.getOrDefault(x, 0) + 1);`     |
| Index mapping    | Store index of an element for quick lookup    |
| Anagram problems | Key = sorted string, Value = list of anagrams |
| Subarray sums    | Key = prefix sum, Value = index               |

```java

HashMap<Integer,String> map = new HashMap<>(); // creating hashmap

map.put(key,value); // key must be unique existing key will be updated.
map.containsKey(key); // checks of key is present

map.get(key); // get the value
map.remove(key); // remove entry

map.clear();

map.keySet(); // returns all the keys

map.values(); // gives all values

// iterating

for(Integer each:map.KeySet()){
	System.out.println(map.get(each));
}
```

HashMap is key value data structure that stores using hashing of keys.


> [!NOTE] Working
> - Internally uses **array of buckets**   
> - Each bucket is a **LinkedList (Java 7)** or **Balanced Tree (Java 8+ for many collisions)**  
> - Hash code of the key determines which bucket the pair goes into
> - Compute `hashCode()` of the key.
> - Map it to a bucket index: `hash % capacity`.
> - Store entry as a `Map.Entry<K, V>` object.
> - Initially via **chaining** (LinkedList).
> - In Java 8+, if collisions in a bucket exceed 8, switches to a **balanced tree (Red-Black Tree)**.

To use custom object as key. We must override equals and hashCode() function 

```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Overriding equals()
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person p = (Person) o;
        return age == p.age && name.equals(p.name);
    }

    // Overriding hashCode()
    @Override
    public int hashCode() {
        return name.hashCode() + 31 * age;
    }
}
```

Remember that every class is subclass of Object and Object has these two methods.

### HashSet:

A **`HashSet<E>`** is a collection that **stores unique elements only** (no duplicates).

| Method          | Description                     |
| --------------- | ------------------------------- |
| `add(E e)`      | Adds the element if not present |
| `remove(E e)`   | Removes the element             |
| `contains(E e)` | Returns true if present         |
| `isEmpty()`     | Checks if the set is empty      |
| `size()`        | Returns number of elements      |
| `clear()`       | Removes all elements            |
| `iterator()`    | Returns iterator for traversal  |

### TreeSet:

| Method          | Description                                |
| --------------- | ------------------------------------------ |
| `add(E e)`      | Adds element (throws if null or duplicate) |
| `remove(E e)`   | Removes element                            |
| `contains(E e)` | Checks presence                            |
| `isEmpty()`     | Checks if set is empty                     |
| `size()`        | Number of elements                         |
| `clear()`       | Clears all elements                        |
| `first()`       | Smallest element                           |
| `last()`        | Largest element                            |
| `ceiling(E e)`  | Smallest ≥ e                               |
| `floor(E e)`    | Largest ≤ e                                |
| `higher(E e)`   | Strictly greater                           |
| `lower(E e)`    | Strictly less                              |
| `pollFirst()`   | Removes and returns first                  |
| `pollLast()`    | Removes and returns last                   |

```java

TreeSet<String> animals = new TreeSet<>();
animals.add("Dog");
animals.add("Cat");

for (String animal : animals) {
    System.out.println(animal);
}

animals.first() // first
animals.last() // largest element
```


> [!NOTE] Note
> **"Poll"** is a term from **queue-based APIs**, meaning: _retrieve and remove the head (or relevant) element_.
> Since `TreeSet` has a sorted order (like a priority queue), this term is used similarly.

```java
// all three sets are iterable
for (String item : set) {
    System.out.println(item);
}
Iterator<String> it = set.iterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

#### Custom ordering in treeSet

```java

// using comparators
TreeSet<Person> set = new TreeSet<>(Comparator.comparing(p -> p.name));

// pass a comparator
Comparator<Person> comp = Comparator.comparing((Person p) -> p.age).thenComparing(p -> p.name);

TreeSet<Person> set = new TreeSet<>(comp);

// or using lambda function
TreeSet<Person> people = new TreeSet<>((p1, p2) -> p1.age - p2.age);
```

