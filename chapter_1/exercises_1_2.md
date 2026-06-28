# 1.2-1 Give an example of an application that requires algorithmic content at the application level, and discuss the function of the algorithms involved.

- One example would be a warehouse management system where the system will need to run an algorithm to compute the best place to put the materials you need to store. You might need an algorithim to take the materials with its dimensions and compute what would be the best place in storage to put it.
- Another example would be a map application that calculates routes. Shortest path would be an example of algorithm used in that application.
- Yet another would be a calendar application that runs an algorithm to find the best time slot for a meeting considering all other events in the calendar of the attendees.

# 1.2-2 Suppose we are comparing implementations of insertion sort and merge sort on the same machine. For inputs of size n, insertion sort runs in 8n2 steps, while merge sort runs in 64n lg n steps. For which values of n does insertion sort beat merge sort?

https://www.geogebra.org/calculator/tpekvaym

8*(n^2) < 64 * n * lg(n)    // div 8
n^2     < 8 * n * lg(n)     // div n
n       < 8 * lg(n)

Transcendental equation. Best option seems to test values of n if we don't want to resort to more complex things like the Lambert W function.

Testing powers of 2 for n:

n = 8  |  8 < 8 * lg(8)  |  8 < 8 * 3 |  8 < 24 | True
n = 16 | 16 < 8 * lg(16) | 16 < 8 * 4 | 16 < 32 | True
n = 32 | 32 < 8 * lg(32) | 32 < 8 * 5 | 32 < 40 | True
n = 64 | 64 < 8 * lg(64) | 64 < 8 * 6 | 64 < 48 | False

There is a value of n bewteen 32 and 64 that is the transition point. Meaning that for values of n less than this value insertion sort will beat merge sort. If we are willing to use a calculator to compute logs of non-powers of 2, we can get to the transition point which is 43.


# 1.2-3 What is the smallest value of n such that an algorithm whose running time is 100n2 runs faster than an algorithm whose running time is 2^n on the same machine?

https://www.geogebra.org/calculator/nv5ajuqg

100 * n^2 < 2^n

n = 1 | 100 * 1^2 < 2^1 | 100 < 2 | False
...
// 128 (2^7) is the first power of 2 larger than 100, so lets try it
n = 7 | 100 * 7^2 < 2^7 | 4900 < 128 | False
...
// 8192 (2^13) fist power of 2 > 4900
n = 13 | 100 * 13^2 < 2^13 | 16900 < 8192  | False
n = 14 | 100 * 14^2 < 2^14 | 19600 < 16384 | False
n = 15 | 100 * 15^2 < 2^15 | 22500 < 32768 | True

15 is the smaller integer value of n such that the first alg runs faster than the second one.

# 1-1 Comparison of running times
## For each function f .n/ and time t in the following table, determine the largest size n of a problem that can be solved in time t, assuming that the algorithm to solve the problem takes f .n/ microseconds.