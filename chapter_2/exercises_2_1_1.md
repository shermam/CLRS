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

# 2.1-3 Consider the searching problem:

- **Input:** A sequence of n numbers A = {a1, a2,...,an} and a value v.
- **Output:** An index i such that v = A[i] or the special value NIL if v does not appear in A.

**Write pseudocode for linear search, which scans through the sequence, looking for v.**

```
LINEAR SEARCH(A, v)
1 for i = 1 to A.length
2   if A[i] == v
3     return i
4 return NIL
```

 **Using a loop invariant, prove that your algorithm is correct. Make sure that your loop invariant fulfills the three necessary properties.**

 **LOOP INVARIANT:** At the start of each iteration of the `for` loop, the subarray A[1..i-1] does NOT contain the value v.

 **Initialization:** We initialize i to 1, so the subarray A[1..i-1] represents A[1..0], which is empty, and therefore doesn't contain any value, including v.

 **Maintenance:** For each iteration we check if the value at position i is equal to v. If it is we break out of the loop with the `return` keyword. This means that each iteration either maintains the invariant and goes to the next iteration or breaks the loop.

 **Termination:** The loop terminates either:
 - when the check on line 2 is `true` and we find the value. In which case we exit out of the loop and `i` is not incremented anymore. This means A[1..i-1] still doesn't contain v and is the largest subarray prefix that doesn't contain v, because A[i] is equal to v. This branch shows correctness by outputing `i` (line 3) such that `v = A[i]`.
 - or when `i > A.length` meaning that the check on line 2 was false for all previous iterations. And therefore A[1..i-1] represents the entirety of A, which in this case doesn't contain v. This branch shows correctness by outputing NIL (line 4) indicating that v does not appear in A.

# 2.1-4 Consider the problem of adding two n-bit binary integers, stored in two n-element arrays A and B. The sum of the two integers should be stored in binary form in an (n+1)-element array C. State the problem formally and write pseudocode for adding the two integers.

## Binary sum:

**Input:** `A` and `B`, which are sequences of `n` binary digits `A = {a1, a2,..., an}` and `B = {b1, b2,..., bn}`, where each element of the sequence is either `0` or `1`. `A` and `B` therefore represent n-bit binary integers, where the first element in the sequence is the Most Significant Bit.

**Outpu:** A sequence `C` of (n+1) binary digits `C = {c1, c2,..., cn, cn+1}` which represents the sum `A` and `B`

Pseudo code: 

ADDER(A, B)
```
carry = 0
C = [A.length + 1]
for i = A.length downto 1:
  C[i+1] = (A[i] != B[i]) != carry
  carry = (A[i] and B[i]) or (carry and (A[i] != B[i]))
C[1] = carry
return C
```

Note that we run the loop backwards because the first element in the sequence is the most significant bit.

**LOOP INVARIANT:** At the start of the iteration of the `for` loop, the subarray C[i+2..A.length+1] contains the last `m` bits (where `m` = A.length - i) of the sum of the numbers represented by the subarrays A[i+1..A.length] and B[i+1..A.length].

**Initialization:** We initialize i to Array.length so `m` would be 0, and C[i+2..A.length+1], A[i+1..A.length] and B[i+1..A.length] are all empty subarrays. Therefor C[i+2..A.length+1], which is empty, contains the sum of A[i+1..A.length] and B[i+1..A.length] which are also empty.

**Maintenance:** In each iteration we populat the position `i+1` of C with the bit that represents the sum of A[i] and B[i] maintaing invariant.

**Termination:** We exit the loop when i reaches 0, and therefore the sequence C[2..A.length+1] contains the first `n` bits of the sum of A[1..A.lenght] and B[1..A.lenght], which are the full numbers. Therefore when we finally put the carry bit at position `1` of C, C will contain the full sum of A and B.