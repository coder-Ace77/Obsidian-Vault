Here's a refined and unambiguous version of your document with corrected grammar, clarified problem statements, and added sample test cases:

---

## Logical Reasoning Prerequisite: Arrays, Strings

---

###  Good Integer 1

**Definition:**  
Let `f(x)` be the sum of digits of integer `x`. An integer `x` is called **good** if `f(x) = x`.  
Your task is to determine whether a given integer is good or not.

**Input:**

- The first line contains a single integer `t` — the number of test cases.
    
- Each of the next `t` lines contains a single integer `x` (`1 ≤ x ≤ 10^9`).
    

**Output:**

- For each test case, print `"YES"` if the number is good, otherwise print `"NO"`.
    

**Sample Input:**

```
3
0
9
10
```

**Sample Output:**

```
YES
YES
NO
```

---

### Good Integer 2

**Definition:**  
Same as **Good Integer 1**, but now `x` can be extremely large (up to 1000 digits), so you must handle the number as a string.

**Input:**

- The first line contains a single integer `t` — the number of test cases.
    
- Each of the next `t` lines contains a single string representing an integer `x` (`1 ≤ |x| ≤ 1000`), where `|x|` is the number of digits.
    

**Output:**

- For each test case, print `"YES"` if the number is good, otherwise print `"NO"`.
    

**Sample Input:**

```
2
0
999999999999
```

**Sample Output:**

```
YES
NO
```

---

### MEX Theory

**Definition:**  
The **MEX** (Minimum Excluded) of an array is the smallest non-negative integer that is not present in the array.

You are given an array and can perform the following operation any number of times:

- Choose any element and increase it by 1.
    

Find the **minimum number of operations** required to **minimize the MEX** of the array.

**Input:**

- The first line contains an integer `t` — the number of test cases.
    
- For each test case:
    
    - The first line contains a single integer `n` (`1 ≤ n ≤ 10^5`) — the size of the array.
        
    - The second line contains `n` integers `a[i]` (`0 ≤ a[i] ≤ 10^9`).
        

**Output:**

- For each test case, print a single integer — the minimum number of operations required.
    

**Sample Input:**

```
2
5
0 1 2 3 5
4
0 2 2 3
```

**Sample Output:**

```
1
1
```

---

## Prefix/Suffix Sums

---

### Pair Power

You are given an array `a` of `n` integers. Define the **power** of the array as the number of pairs `(i, j)` such that:

```
a[i] - a[j] ≤ k   where 1 ≤ i, j ≤ n
```

Note that pair(i,j) and pair(j,i) should be counted as 1.

**Input:**

- The first line contains an integer `t` — the number of test cases.
    
- For each test case:
    
    - The first line contains two integers `n` and `k` (`1 ≤ n ≤ 10^5`, `0 ≤ k ≤ 10^9`).
        
    - The second line contains `n` integers `a[i]` (`|a[i]| ≤ 10^9`).
        

**Output:**

- For each test case, print a single integer — the number of valid pairs.
    

**Sample Input:**

```
1
5 2
1 3 5 7 9
```

**Sample Output:**

```
4
```

---

### Finding Alive

You are given an array representing the health of `n` monsters. Each second, every monster’s health decreases by `1`. A monster dies when its health becomes `0` or below.

You are given `q` queries. In each query, you are given a time `t` and asked how many monsters are still alive at that time.

**Input:**

- The first line contains an integer `t` — the number of test cases.
    
- For each test case:
    
    - The first line contains two integers `n` and `q` (`1 ≤ n, q ≤ 10^5`).
        
    - The second line contains `n` integers `h[i]` — the initial health of each monster (`1 ≤ h[i] ≤ 10^9`).
        
    - The next `q` lines each contain a single integer `t[i]` (`0 ≤ t[i] ≤ 10^9`) — the time of the query.
        

**Output:**

- For each query, print a single integer — the number of monsters alive at time `t[i]`.
    

**Sample Input:**

```
1
5 3
1 3 2 4 2
0
2
3
```

**Sample Output:**

```
5
2
1
```

---

###  Finding Alive 2

Same as **Finding Alive**, but with an additional twist: an **evil scientist** can increase the health of any monster at a specific time `t`.  
However, dead monsters cannot be revived.

There are two types of queries:

1. `1 t i x` — At time `t`, increase the health of monster at index `i` (1-based) by `x`.
    
2. `2 t` — At time `t`, report how many monsters are still alive.
    

**Input:**

- The first line contains an integer `t` — the number of test cases.
    
- For each test case:
    
    - The first line contains two integers `n` and `q` (`1 ≤ n, q ≤ 10^5`).
        
    - The second line contains `n` integers `h[i]` (`1 ≤ h[i] ≤ 10^9`) — initial health of monsters.
        
    - The next `q` lines describe the queries:
        
        - Either `1 t i x` (`1 ≤ i ≤ n`, `1 ≤ x ≤ 10^9`, `0 ≤ t ≤ 10^9`)
            
        - Or `2 t` — a query asking how many monsters are alive at time `t`.
            

**Output:**

- For each query of type 2, print a single integer — the number of monsters alive at that time.
    

**Sample Input:**

```
1
3 5
3 2 1
2 1
1 1 2 5
2 2
1 2 3 2
2 3
```

**Sample Output:**

```
2
3
2
```

---

Let me know if you'd like reference solutions or complexity analysis for these problems.