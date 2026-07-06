# 2.2-1 Express the function $n^3/1000 - 100n^2 - 100n + 3$ in terms of $\Theta$-notation.

$\Theta(n^3)$

Reasoning: I took the highest order term ($n^3/1000$) and removed the constant factor 1000, leaving only $n^3$. And then just presented it wrapped up in parentheses next to the Theta greek letter as seems to be the convention.

# 2.2-2 Consider sorting n numbers stored in array A by first finding the smallest element of A and exchanging it with the element in A[1]. Then find the second smallest element of A, and exchange it with A[2]. Continue in this manner for the first n-1 elements of A. Write pseudocode for this algorithm, which is known as selection sort.

```
for j=1 to A.length-1:
  smallest_index = j
  for i=j+1 to A.length:
    if a[i] < a[smallest_index]:
      smallest_index = i
  a[j], a[smallest_index] = a[smallest_index], a[j]
```

## What loop invariant does this algorithm maintain?

At the start of the iteration of the `for` loop, the subarray A[1..j-1] contains the smallest j-1 elements of array A in non-decreasing order.

**Initialization:** At the start of the algorithm `j` is initialized to 1. Therefore A[1..0] is empty and contains the `0` (j-1) elements of array A in non-decreasing order.

**Maintenance:** On every iteration we find the smallest element found in the subarray A[j..A.length] and put it in A[j]. Since we don't touch any of the elements from the subarray A[1..j-1], which contains the smallest elements picked on previous iterations, we maintain the loop invariant.

**Termination:** We terminate the loop when `j = A.length` and therefore doesn't not satisfy the check of `j <= A.length-1` from line 1. At this point we know from the invariant that the subarray A[1..A.length-1] is sorted. This accounts for almost all elements of A with the exception of the last element. But at this point the element in the last position was not picked as the smallest in any of the previous iterations. Which means that it is not smaller than any of the previous elements and is the in the right sorted place. Therefore the whole array is sorted.

## Why does it need to run for only the first n  1 elements, rather than for all n elements?

See termination above for explanation.

## Give the best-case and worst-case running times of selection sort in $\Theta$-notation.

We let $t_j$ be the number of times the the expression in the `if` statement on line `4` evaluates to `True` for that value of `j`. 

|SELECTION-SORT(A)                                        |Cost   |times                       |
|:--------------------------------------------------------|:------|:---------------------------|
|`1.for j=1 to A.length-1:`                               | $c_1$ | $n$                        |
|`2...smallest_index = j`                                 | $c_2$ | $n-1$                      |
|`3...for i=j+1 to A.length:`                             | $c_3$ | $\sum_{j=1}^{n-1} (n-j+1)$ |  
|`4....if a[i] < a[smallest_index]:`                      | $c_4$ | $\sum_{j=1}^{n-1} (n-j)$   |
|`5......smallest_index = i`                              | $c_5$ | $\sum_{j=1}^{n-1} t_j$     |
|`6...a[j], a[smallest_index] = a[smallest_index], a[j]`  | $c_6$ | $n-1$                      |

Then the whole running time can be calculated as follow:

$T(n) = c_1n + c_2(n-1) + c3\sum_{j=1}^{n-1} (n-j+1) + c_4\sum_{j=1}^{n-1} (n-j) + c_5\sum_{j=1}^{n-1} t_j + c_6(n-1)$

For this algorithm, $t_j$ is the only thing that can vary from best-case to worst-case.

### Best Case

By changing the arrangement of elements in A we can minimize the number of times that line 5 is executed.

We can set the initial position of the elements to be sorted in nondecreasing order. This way, all of the comparisons that we do on line 4 will be false since we compare elements in earlier positions to elements in later positions. This means line 5 will never be executed and can be removed from the cost calculation. $t_j = 0$

$T(n) = c_1n + c_2(n-1) + c_3\sum_{j=1}^{n-1} (n-j+1) + c_4\sum_{j=1}^{n-1} (n-j) + c_6(n-1)$

Remembering some basic sumation formulas:

- $\sum\limits_{k=1}^{n} k = \frac{n(n+1)}{2}$

Expanding the first summation:

$\sum_{j=1}^{n-1} (n-j+1) = \sum_{j=1}^{n-1} n - \sum_{j=1}^{n-1} j + \sum_{j=1}^{n-1} 1$

Now simplifying each of the 3 parts:

1. $\sum_{j=1}^{n-1} n = n(n-1)$
2. $\sum_{j=1}^{n-1} j = \frac{(n-1)((n-1)+1)}{2} = \frac{n(n-1)}{2}$
3. $\sum_{j=1}^{n-1} 1 = n-1$

Putting them together and grouping like terms we have:

$(n(n-1)) - (\frac{n(n-1)}{2}) + (n-1)$

$= (n^2-n) - (\frac{n^2-n}{2}) + (n-1)$ 

$= n^2-n-\frac{1}{2}(n^2-n)+n-1$

$= n^2-\frac{1}{2}(n^2-n)-1$

$= n^2-\frac{1}{2}n^2+\frac{1}{2}n-1$

$= \boxed{\frac{1}{2}n^2+\frac{1}{2}n-1}$

Now expanding the second summation:

$\sum_{j=1}^{n-1} (n-j) = \sum_{j=1}^{n-1} n - \sum_{j=1}^{n-1} j$

And again:

1. $\sum_{j=1}^{n-1} n = n(n-1)$
2. $\sum_{j=1}^{n-1} j = \frac{(n-1)((n-1)+1)}{2} = \frac{n(n-1)}{2}$

and we have then:

$(n(n-1)) - (\frac{n(n-1)}{2})$

$= (n^2-n) - (\frac{n^2-n}{2})$ 

$= n^2-n-\frac{1}{2}(n^2-n)$

$= n^2-n-\frac{1}{2}n^2+\frac{1}{2}n$

$= \boxed{\frac{1}{2}n^2-\frac{1}{2}n}$

Substituting on the main expression:

$T(n) = c_1n + c_2(n-1) + c_3(\frac{1}{2}n^2+\frac{1}{2}n-1) + c_4(\frac{1}{2}n^2-\frac{1}{2}n) + c_6(n-1)$

$= c_1n+c_2n-c_2+\frac{1}{2}c_3n^2+\frac{1}{2}c_3n-c_3+\frac{1}{2}c_4n^2-\frac{1}{2}c_4n+c_6n-c_6$

$= (\frac{1}{2}c_3+\frac{1}{2}c_4)n^2+(c_1+c_2+\frac{1}{2}c_3-\frac{1}{2}c_4+c_6)n-(c_2+c_3+c_6)$

Now we can already extract the constants like:
- $a = \frac{1}{2}c_3+\frac{1}{2}c_4$
- $b = c_1+c_2+\frac{1}{2}c_3-\frac{1}{2}c_4+c_6$
- $c = c_2+c_3+c_6$

Which leaves us with the degree 2 polinomial:

$an^2+bn-c$

Removing lower terms and the leading term constant coeficient we have the running time of the best case expressed as $\boxed{\Theta(n^2)}$.

### Worst Case

Similarly we can maximize the number of times line 5 is executed by rearranging the elements in the initial position of the array.
We now arrange elements in nonincreasing order, which ensures that the expression on line 4 will always yield True, and line 5 will be executed as many times as line 4. The whole calculation will then look like this for ($t_j = (n-j)$):

$T(n) = c_1n + c_2(n-1) + c_3\sum_{j=1}^{n-1} (n-j+1) + c_4\sum_{j=1}^{n-1} (n-j) + c_5\sum_{j=1}^{n-1} (n-j) + c_6(n-1)$

Expanding summations for this:

$\sum_{j=1}^{n-1} (n-j+1)$ like before $= \boxed{\frac{1}{2}n^2+\frac{1}{2}n-1}$

and $\sum_{j=1}^{n-1} (n-j) = \boxed{\frac{1}{2}n^2-\frac{1}{2}n}$

Then we have:

$T(n) = c_1n + c_2(n-1) + c_3(\frac{1}{2}n^2 + \frac{1}{2}n - 1) + c_4(\frac{1}{2}n^2-\frac{1}{2}n) + c_5(\frac{1}{2}n^2-\frac{1}{2}n) + c_6(n-1)$

$=c_1n + c_2n - c_2 + \frac{1}{2}c_3n^2 + \frac{1}{2}c_3n - c_3 + \frac{1}{2}c_4n^2 - \frac{1}{2}c_4n + \frac{1}{2}c_5n^2 - \frac{1}{2}c_5n + c_6n - c_6$

$=(\frac{1}{2}c_3 + \frac{1}{2}c_4 + \frac{1}{2}c_5)n^2 + (c_1 + c_2 + \frac{1}{2}c_3 - \frac{1}{2}c_4 - \frac{1}{2}c_5 + c_6)n - (c_2 + c_3 + c_6)$

Taking the constants like this:
- $a = \frac{1}{2}c_3 + \frac{1}{2}c_4 + \frac{1}{2}c_5$
- $b = c_1 + c_2 + \frac{1}{2}c_3 - \frac{1}{2}c_4 - \frac{1}{2}c_5 + c_6$
- $c = c_2 + c_3 + c_6$

We again have the degree 2 polinomial:

$an^2+bn+c$ which in Theta notation is represented by $\boxed{\Theta(n^2)}$.

So, diferently from Insertion Sort, Selection sort has running time proportional to $\boxed{\Theta(n^2)}$ for both, the best case and worst case.

