# Lab 4: Concept Review

This lab reviews the foundational concepts of algorithms and data structures that we have covered in the first half of the course. 

**Instructions:** To complete this lab, you may work in groups, but you must write your solutions yourself. Choose two of the topics below that you need to review and complete the corresponding problems. Where relevant, you are given the answer and must provide the justification as your solution. Once you have completed the lab, push your changes to your forked repository.

**Topics:** asymptotic analysis, data structures, empirical comparison of algorithms, pseudocode, greedy algorithms. 

## Asymptotic Analysis

1. Use the rules from lecture 07 to prove that $T(n) = 5 \log n + 7n$ is $\mathcal{O}(n)$.

**Answer**: $T(n) = \mathcal{O}(n)$.

**Justification**: For all $n \ge 1$, we know $\log n \le n$. Therefore,

$$
5\log n + 7n \le 5n + 7n = 12n.
$$

This matches the definition of $\mathcal{O}(n)$ because a constant multiple of $n$ is still $\mathcal{O}(n)$. The linear term $7n$ dominates the logarithmic term $5\log n$, so the function grows no faster than a constant times $n$.

2. True/False/Possibly: $T(n)$ is $\mathcal{O}(n^2)$?

**Answer**: Yes

**Justification**: Since $T(n) = \mathcal{O}(n)$, it is also $\mathcal{O}(n^2)$ because $n^2$ grows faster than $n$. For sufficiently large $n$, $n \le n^2$, so any function that is linear is automatically bounded above by a quadratic function.

3. True/False/Possibly: $T(n)$ is $\Omega(n \log n)$?

**Answer**: No

**Justification**: A function is $\Omega(n\log n)$ only if it grows at least as fast as $n\log n$. But $T(n) = 5\log n + 7n$ is essentially linear in growth, while $n\log n$ grows faster than $n$. Therefore, $T(n)$ does not have a lower bound of $n\log n$.

4. For any algorithm, we can give a trivial lower bound. What is that lower bound?

**Answer**: $\Omega(1)$

**Justification**: Every algorithm must perform at least some work to finish, even when the input is very small. So no algorithm can have a running time below constant time in the worst case or best case, which gives the universal lower bound $\Omega(1)$.

5. Is there a corresponding trivial upper bound? Why or why not?

**Answer**: No

**Justification**: There is no single constant-time upper bound that applies to every algorithm because different algorithms can take very different amounts of time as the problem size grows. Some algorithms are $\mathcal{O}(1)$, others are $\mathcal{O}(\log n)$, others $\mathcal{O}(n)$, and others much slower. Because the runtime can vary by algorithm, there is no universal trivial upper bound of $\mathcal{O}(1)$ for all algorithms.


## Data Structures

1. You are programming a robot to navigate a maze. As the robot moves forward, it records each intersection it passes. When it hits a dead end, it needs to retreat to the most recently visited intersection to try a different path.

**Answer**: Stack

**Justification**: A stack uses LIFO (Last In, First Out) order. The robot keeps adding the most recent intersection to the top, and when it backtracks, it goes to the last place it visited. That matches stack behavior exactly.

2. A server receives a massive influx of data packets from a streaming video application. To prevent the video from skipping or playing out of order on the user's end, the server must process and forward these packets in the exact sequence they were received.

**Answer**: Queue

**Justification**: A queue uses FIFO (First In, First Out) order. The packet that arrives first must be processed and sent first, so the order is preserved and the video plays correctly.

3. An atmospheric monitoring system reads temperature data from 10,000 sequentially numbered sensors (IDs 0 through 9999). Throughout the day, the system needs to constantly update and read the current temperature of randomly selected sensors based on their ID number to build localized weather maps.

**Answer**: Array

**Justification**: An array allows direct access by index. Since each sensor has a numeric ID, the program can instantly access or update the value for any sensor by its ID number. This makes arrays ideal for random access in a fixed-size collection of numbered items.

4. You are building a lightweight syntax checker for a code editor. Its sole job is to scan a document and ensure that every opened parenthesis `(`, bracket `[`, and brace `{` is matched with its corresponding closing character in the correct nested order.

**Answer**: Stack

**Justification**: A stack is used to match nested symbols because the most recently opened symbol must be the next one closed. When an opening symbol appears, it is pushed onto the stack. When a closing symbol appears, the matching opening symbol is popped. This behavior is exactly what a stack provides.

## Empirical Comparison of Algorithms

1. A student is benchmarking an algorithm that takes a list as its input. They run it on progressively larger randomly generated lists, doubling the number of elements ($n$) and record the following execution times:

- $n = 1000$: 0.12 seconds
- $n = 2000$: 0.94 seconds
- $n = 4000$: 7.61 seconds
- $n = 8000$: 60.85 seconds

 Based on this empirical data, what is the most likely asymptotic time complexity of the algorithm? **Hint**: Calculate the doubling ratio between each pair of consecutive runs.

 **Answer**: Cubic time complexity, $\mathcal{O}(n^3)$

**Justification**:

 2. Two students write separate algorithms to compute a metric over an array of 10 million integers. Both algorithms perform exactly one mathematical operation per element, meaning both have a theoretical time complexity of $O(N)$. However, during benchmarking, Algorithm A consistently runs 15x faster than Algorithm B. Why might theoretical Big-O analysis fail to predict this massive performance gap? 

**Answer**:

 3. Scenario: To measure the running time of algorithms for an empirical comparison, a developer writes the following benchmarking script:

```python
import time

large_array = [i for i in range(1000000)]
start = time.time()
myAlg(large_array)
end = time.time()

print("Time:", end - start)
```

They run this script exactly once for each algorithm on their laptop while streaming a movie in the background. Identify at least three distinct methodological flaws in this benchmarking setup that make the results unreliable.

**Answer**:

## Pseudocode

1. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
count = 0
for i = 1 to N do
    for j = i to N do
        do_work()
```

Write a closed-form expression for the number of times `do_work()` is called in terms of $N$.

2. Analyze the exact number of times the `do_work()` function is called in the following pseudocode, assuming $N \ge 1$.

```
i = N
while i > 0:
    for j = 1 to i:
        do_work()
    i = floor(i / 2)
```

If $N=16$, how many times is `do_work()` called?

**Answer**: 31

**Justification**:

## Greedy Algorithms

You are organizing a film festival but only have access to a single screen. You are given a list of $n$ films, each with a specific `start_time` and `end_time`. You want to screen the maximum number of films possible.

Consider the following three greedy strategies:

- **Shortest First**: Always pick the film with the shortest duration (that doesn't conflict with already chosen films).
- **Earliest Start**: Always pick the film that starts the earliest (that doesn't conflict).
- **Earliest Finish**: Always pick the film that finishes the earliest (that doesn't conflict).

Which of these three strategies guarantees an optimal solution (maximum number of films)? For the two strategies that fail, provide a counter-example (a small set of film times) where the greedy choice results in a sub-optimal schedule.

**Answer**: The earliest finish strategy guarantees an optimal solution.

**Justification**: