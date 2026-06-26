# 1.1-1 Give a real-world example that requires sorting or a real-world example that requires computing a convex hull.

 - Sorting: Books in a shelf of a library
 - Convex Hull: Maybe finding people close to the edge of a big crowd, maybe?

# 1.1-2 Other than speed, what other measures of efficiency might one use in a real-world setting?

- Space usage
- Resource usage
- Correctness (error rate)

# 1.1-3 Select a data structure that you have seen previously, and discuss its strengths and limitations.

Arrays. They are very basic structures, but powerful in the way they represent the underlying memory.

Strenghs:
- Allow retrival of random elements in O(1) given an index.
- Represent a sequential chunk of memory, therefore traversal is quick, as the memory should be loaded in chunks.
- Ubiquitous in basically all programming languages.

Limitations:
- Size needs to be allocated up-front. Some programing languages will do the heavy lifiting of growing an array for you under the hood when you try to grow it dynamically, but in general this is outside the primary scope of that data structure.
- Because it represents a contiguous chunk of memory, each element must have a well defined size. (Those can, however, be pointers to other parts of memory that contain objects of arbitrary size.)


# 1.1-4 How are the shortest-path and traveling-salesman problems given above similar? How are they different?

Similarities:
- Both can be represented as graphs with weighted edges.
- The resolution involves minimizing the sum of the weighted edges that forms a path through the nodes that comply with certain contraints.

Differences:
- The constraints for each problem are a bit different:
  - Shortest path is about a path that starts at a specific node and ends at another specific node. The nodes visited in between are not constrained, except for the fact that we have to find the path the minimizes the sum of the weights of the edges used.
  - Traveling Salesman, on the other hand, is about a set of nodes (not only start and end) that MUST be visited by the path. In the example in the book, with the company with a central depot, the path must end where it started, which is also different from Shortest path where start and end are different.

# 1.1-5 Come up with a real-world problem in which only the best solution will do. Then come up with one in which a solution that is “approximately” the best is good enough.

This was a specially tricky one. If for "real-world", we mean "physical world", then almost everything can be approximatted within an allowed margin of error that can be arbitrarily small. For example:

- Fuel calculation for a plane. Altough very critical, it would safelly support errors of a couple of drops of fuel in a tank with hundreds of litters.
- Voting. This is an interesting one, because the error margin can be easily smaller than what would be allowed by the smaller difference in discrete quantities. For example, let's say the acceptable margin of error is of 0.01%:
  - In a company with a board of directors with 10 people that are voting on some decision, the smaller inacuracy is of 1 vote, which represents 10% of total votes. 10% > 0.01%. So in this scenario only the exact solution will do.
  - Now in the elections for president of a country with 100M people. 1 vote represents 0,000001% which is smaller than 0.01%. In that scenario the approximate solution will do.
- Even with money some approximations that accounts for rounding errors are usually acceptable.