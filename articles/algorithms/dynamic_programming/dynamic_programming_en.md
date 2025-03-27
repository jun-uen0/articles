# Dynamic Programming

## Introduction
Dynamic Programming is an efficient algorithm design technique used to solve problems by breaking them down into smaller subproblems.  
It stores the results of these subproblems to avoid redundant work.

It was popularized by Richard Bellman (yes, the same person behind the Bellman-Ford algorithm).

---

# Example: Fibonacci Number

## Fibonacci Number
The Fibonacci sequence is a series of numbers where each number is the sum of the two numbers before it.  
Example: 1, 1, 2, 3, 5, 8, 13, 21 ...

[Wikipedia: Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_sequence)

---

## Naive Recursion Algorithm for Fibonacci Numbers

Here’s a simple recursive solution for calculating F(n):

```py
def fib_naive(n):
    if n <= 2:
        return 1
    else:
        return fib_naive(n - 1) + fib_naive(n - 2)
```

But it’s a bad solution. The time complexity is **O(2ⁿ)** — exponential.   
Let’s count how many times the function is called:

```py
cnt = 0

def fib_naive(n):
    global cnt
    cnt += 1

    if n <= 2:
        return 1
    else:
        return fib_naive(n - 1) + fib_naive(n - 2)

print(fib_naive(20))
print("OMG. Function was called", cnt, "times.")
```

---

## Memoized Algorithm

Not “memo**r**ized,” but **memoized** algorithm 😄  
This version stores each result in a dictionary. If the function tries to calculate the same value again, it just returns the stored result.

```py
def fib_memo(n, memo=None):
    if memo is None: memo = {}                                   # ①
    if n in memo: return memo[n]                                 # ②

    if n <= 2: result = 1                                        # ③
    else: result = fib_memo(n - 1, memo) + fib_memo(n - 2, memo) # ④

    memo[n] = result                                             # ⑤
    return result
```

Explanation:
① On the first call, we create an empty dictionary.  
② If we’ve already computed this `n`, just return it.  
③ Base case: F(1) and F(2) are both 1.  
④ Same logic as the naive version, but with memoization.  
⑤ Store the result to avoid recalculating next time.  
  
Let’s count how many times this one runs:  

```py
cnt = 0

def fib_memo(n, memo=None):
    global cnt
    cnt += 1

    if memo is None: memo = {}
    if n in memo: return memo[n]

    if n <= 2: result = 1
    else: result = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)

    memo[n] = result

    return result

print(fib_memo(20))
print("Yep. Function was called only", cnt, "times.")
```

Time complexity is **O(n)**, and space complexity is also **O(n)** due to the memo dictionary and recursion stack.

---

## Bottom-Up DP | Time: O(n), Space: O(1)

Memoized version is efficient, but we can go further!  
Memoized and naive versions both calculate **top-down**, but we humans usually think **bottom-up** — starting from the base.

With bottom-up DP, we can also reduce space to **O(1)** by only storing the last two values.

```py
def fib_bottom_up_O1(n):
    if n <= 2: return 1

    prev, curr = 1, 1

    for k in range(2, n):
        prev, curr = curr, prev + curr

    return curr
```

- We iterate from 2 to `n`
- Use only two variables: `prev` and `curr`
- Super fast and memory-efficient!

---

## Bottom-Up DP | Time: O(n), Space: O(n)

The O(1) version is great if we just need **F(n)**.  
But what if we want the **entire Fibonacci sequence** up to n?

```py
def fib_bottom_up_On(n):
    if n == 1: return [1]
    if n == 2: return [1, 1]

    fib = [0] * n
    fib[0], fib[1] = 1, 1

    for k in range(2, n):
        fib[k] = fib[k - 1] + fib[k - 2]

    return fib
```

Now we store all values in an array, which takes **O(n)** space.

---

## 2D DP Table (Tabulation) | Time: O(m × n), Space: O(m × n)

2D DP Table (Tabulation) | Time: O(m × n), Space: O(m × n)
When solving problems involving two inputs (like two strings), we often use a 2D DP table to store the solutions to subproblems. Each cell dp[i][j] stores the result of solving the problem for the first i characters of text1 and the first j characters of text2.

A classic example is the Longest Common Subsequence:

```py
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    
    # Create a (m+1) x (n+1) DP table initialized with 0
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Build the table from top-left to bottom-right
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i - 1] == text2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]  # characters match
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])  # carry forward the max

    return dp[m][n]  # bottom-right cell has the final result
```

- dp[i][j] means: the length of the LCS between text1[:i] and text2[:j]
- We initialize the table with an extra row and column to handle base cases (i == 0 or j == 0)
- If characters match, we move diagonally.
- If not, we take the best result from the left or top.

Visualization:

```
    ""  a  c  b  e
""  0  0  0  0  0
a   0  1  1  1  1
b   0  1  1  2  2
c   0  1  2  2  2
```

This approach is very powerful and can be extended to:

- Edit Distance
- Knapsack Problems
- Palindrome Substrings

---

## Summary

Dynamic Programming is a powerful technique for solving problems efficiently — especially when the problem has:
- **Overlapping subproblems**
- **Optimal substructure**

There are many ways to implement it:
- Naive recursion (slow)
- Top-down with memoization (fast, readable)
- Bottom-up (faster, less memory)
- Bottom-up optimized (O(1) space!)
- 2D DP Table (Tabulation) (powerful for two inputs)

It depends on **what you want to get**: just the final result? All intermediate values?  
Pick the approach that fits your case.

There are also more advanced applications like:
- Shortest paths in graphs (Dijkstra, Bellman-Ford, etc.)
- Knapsack problems
- Edit Distance
- Game Theory and more

[Wikipedia: Dynamic Programming](https://en.wikipedia.org/wiki/Dynamic_programming)

---

## How can this be applied to real-world problems?

- Calculating shortest paths in maps (e.g. Google Maps, navigation)
- Optimizing stock profits, budgeting, and scheduling
- Predictive text algorithms (e.g. edit distance for spelling correction)
- Game AI — finding optimal moves
- DNA sequence alignment
- Image compression
- Text segmentation

---

## How does it compare with alternative approaches?

| Approach            | Time | Space | Notes                          |
|---------------------|------|-------|--------------------------------|
| Naive Recursion     | O(2ⁿ) | O(n)  | Easy to write, super slow     |
| Memoization         | O(n)  | O(n)  | Fast, readable, recursive     |
| Bottom-Up (Tabulation) | O(n)  | O(n)  | Faster, iterative             |
| Bottom-Up Optimized | O(n)  | O(1)  | Fastest, least memory usage   |
| 2D DP Table (Tabulation) | O(m × n) | O(m × n) | Powerful for two inputs      |

---

## When should I **not** use DP?

- If the problem has **no overlapping subproblems**
- If a **greedy or divide-and-conquer** solution is simpler and faster
- If the problem constraints are small enough that brute force is acceptable

---

## Reference

I studied the overview of Dynamic Programming from this amazing MIT lecture on YouTube:  
Thanks to MIT for sharing such great content for free!

[YouTube: Lecture 19 — Dynamic Programming I: Fibonacci, Shortest Paths](https://youtu.be/OQ5jsbhAv_M?si=TEhHy3YZJWpna8Eg)