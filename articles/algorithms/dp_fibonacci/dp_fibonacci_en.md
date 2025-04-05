# Dynamic Programming: Fibonacci Numbers

## Introduction
Dynamic Programming is an efficient algorithm design technique used to solve problems by breaking them down into smaller subproblems.
It stores the results of these subproblems to avoid redundant work.

## Naive Recursion Algorithm for Fibonacci Numbers
```python
def fib_naive(n):
    if n <= 2:
        return 1
    else:
        return fib_naive(n - 1) + fib_naive(n - 2)
```

## Memoized Algorithm
```python
def fib_memo(n, memo=None):
    if memo is None: memo = {}
    if n in memo: return memo[n]

    if n <= 2: result = 1
    else: result = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)

    memo[n] = result
    return result
```

## Bottom-Up DP | Time: O(n), Space: O(1)
```python
def fib_bottom_up_O1(n):
    if n <= 2: return 1
    prev, curr = 1, 1
    for k in range(2, n):
        prev, curr = curr, prev + curr
    return curr
```

## Bottom-Up DP | Time: O(n), Space: O(n)
```python
def fib_bottom_up_On(n):
    if n == 1: return [1]
    if n == 2: return [1, 1]

    fib = [0] * n
    fib[0], fib[1] = 1, 1

    for k in range(2, n):
        fib[k] = fib[k - 1] + fib[k - 2]

    return fib
```