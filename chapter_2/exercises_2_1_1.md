# 2.1-1 Using Figure 2.2 as a model, illustrate the operation of INSERTION-SORT on the array A A = {31,41,59,26,41,58}

```
(a)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 31 | 41 | 59 | 26 | 41 | 58 |
        +----+----+----+----+----+----+
              ^  |
              |  |
              |__|

(b)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 31 | 41 | 59 | 26 | 41 | 58 |
        +----+----+----+----+----+----+
                   ^  |
                   |  |
                   |__|
(c)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 31 | 41 | 59 | 26 | 41 | 58 |
        +----+----+----+----+----+----+
         ^ |    ^    ^   ^|
         | |____|____|___||
         |________________|
(d)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 26 | 31 | 41 | 59 | 41 | 58 |
        +----+----+----+----+----+----+
                         ^ |   ^|
                         | |___||
                         |______|
(e)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 26 | 31 | 41 | 41 | 59 | 58 |
        +----+----+----+----+----+----+
                              ^ |   ^|
                              | |___||
                              |______|
(f)
          1    2    3    4    5    6 
        +----+----+----+----+----+----+
        | 26 | 31 | 41 | 41 | 58 | 59 |
        +----+----+----+----+----+----+
```


# 2.1-2 Rewrite the INSERTION-SORT procedure to sort into nonincreasing instead of nondecreasing order.

The only change needed is on line 5. When comparing the value on index i with the key we now check for
less than (<) rather than greater than (>).

```
INSERTION-SORT(A) nonincreasing
1 for j = 2 to A.length
2   key = A[j] 
3   // Insert A[j] into the sorted sequence A[1..j-1]
4   i = j-1
5   while i > 0 and A[i] < key
6    A[i+1] = A[i]
7    i = i-1
8   A[i+1] = key
```