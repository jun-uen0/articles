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

## Summary

Dynamic Programming is a powerful technique for solving problems efficiently — especially when the problem has:
- **Overlapping subproblems**
- **Optimal substructure**

There are many ways to implement it:
- Naive recursion (slow)
- Top-down with memoization (fast, readable)
- Bottom-up (faster, less memory)
- Bottom-up optimized (O(1) space!)

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

---

## How does it compare with alternative approaches?

<img width="591" alt="Screenshot 2025-03-22 at 17 10 05" src="https://github.com/user-attachments/assets/5a68a04f-eaae-48c1-b8a5-c1bb438a5179" />

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
