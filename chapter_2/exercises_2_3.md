# 2.3-1 Using Figure 2.4 as a model, illustrate the operation of merge sort on the array `A=[3,41,52,26,38,57,9,49]`.

```
                          Sorted Sequence
             +----+----+----+----+----+----+----+----+
             |  3 |  9 | 26 | 38 | 41 | 49 | 52 | 57 |
             +----+----+----+----+----+----+----+----+
                 ^                               ^   
                /                                 \    
     +----+----+----+----+               +----+----+----+----+
     |  3 | 26 | 41 | 52 |               |  9 | 38 | 49 | 57 |
     +----+----+----+----+               +----+----+----+----+
         ^             ^                     ^             ^   
        /               \                   /               \  
  +----+----+       +----+----+       +----+----+       +----+----+
  |  3 | 41 |       | 26 | 52 |       | 38 | 57 |       |  9 | 49 |
  +----+----+       +----+----+       +----+----+       +----+----+
    ^     ^           ^     ^           ^     ^           ^     ^  
   /       \         /       \         /       \         /       \   
+----+   +----+   +----+   +----+   +----+   +----+   +----+   +----+
|  3 |   | 41 |   | 52 |   | 26 |   | 38 |   | 57 |   |  9 |   | 49 |
+----+   +----+   +----+   +----+   +----+   +----+   +----+   +----+
```

# 2.3-2 Rewrite the MERGE procedure so that it does not use sentinels, instead stopping once either array L or R has had all its elements copied back to A and then copying the remainder of the other array back into A.

## Original procedure
```
MERGE(A,p,q,r)
n1 = q - p + 1
n2 = r - q
let L[1..n1+1] and R[1..n2+1] be new arrays
for i = 1 to n1
  L[i] = A[p+i-1]
for j = 1 to n2
  R[j] = A[q+j]
L[n1+1] = inf
R[n2+1] = inf
i=1
j=1
for k = p to r
  if L[i] <= R[j]
    A[k] = L[i]
    i = i + 1
  else A[k] = R[j]
    j = j + 1
```

## Rewritten Procedure
```
MERGE(A,p,q,r)
n1 = q - p + 1
n2 = r - q
let L[1..n1] and R[1..n2] be new arrays
for i = 1 to n1
  L[i] = A[p+i-1]
for j = 1 to n2
  R[j] = A[q+j]
i=1
j=1
for k = p to r
  if L[i] <= R[j]
    A[k] = L[i]
    i = i + 1
  else A[k] = R[j]
    j = j + 1
  if i > n1 or j > n2
    break
for i=i to n1
  A[p+j+i] = left[i]
for j=j to n2
  A[p+i+j] = right[j]
```

Explanation: 
- I updated the array declarations removine the +1 in the length that was supposed to leave room for the sentinels. 
- I have also remove the addition of the sentinels. 
- I then added an `if` statement to check if i had passed n1 of j had passed n2. If one of them had already passed their respective subarray lengths, it means that there all elements from that side have already been added, and there is no need to compare items anymore. So we break out of the loop.
- Then we copy the remaning items over to the original array with the last two for loops I have added. Note that I start from the last values of i and j. And it is garanteed that one of them will already be past the end of its subarray. So the check on the loop will fail immediately for one of them. And the other one will have then its remaining items copied over to the original array.
