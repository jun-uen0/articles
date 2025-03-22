# Dynamic Programming
## Introduction
Dynamic Programming is the efficient algorithm to solve the problem.
It breaks down to subproblem for each. It is invented by Bellmen-Ford.

# Example. Fibonacci Number
## Fibonacci Number
The Fibonacci sequence is a series of numbers where each number is the sum of the two numbers before it.
Ex. 1,1,2,3,5,8,13,21 ...

[Wikipedia: Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_sequence)

## Naive recusion algorithm for Fibonacci Number
Here is a simple code to figure F(n) out, calculation of Fibonacci Number.

```py
def fib_naive(n):

    if n <= 2:
        return 1
    else:
        return fib_naive(n - 1) + fib_naive(n - 2)
```

But it is a bad solution. The time complexity is O(2ⁿ).
Let's count up how many time the function called.

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

## Memoized algorithm
Not memo"r"ized, but memoized algorith.
This algorithm store the result for each loop and when the funciton tyies to calculate the same number, it just returns the result alreadly solved.

Here is the code.

```py
def fib_memo(n, memo=None):

    if memo is None: memo = {}                                   # ①
    if n in memo: return memo[n]                                 # ②

    if n <= 2: result = 1                                        # ③
    else: result = fib_memo(n - 1, memo) + fib_memo(n - 2, memo) # ④

    memo[n] = result                                             # ⑤

    return result
```
① First call, memo become the empty dictionary
② This is one of keys of Memoized algorithm. When funciton tries to calculate the same index, it just returns the result already set.
③ Base case of Fibonacci Number, we already know that F(1) and F(2) is 1. And Since we will call F(n - 1) and F(n - 2), we have to start calculation by 3, to avoid loop will be calculate negative values.
④ This is just same as naive one.
⑤ Store the result to memo[n], so that we don't have calculate the same value of n again.

Let's count up the memoized Fibonacci Number.

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

Time complexity is O(n), and also space complexity is 0(n)

## Bottom Up DP | Time complexity: O(n) / Space complexity: O(1)
Memoized algorithm is very effeicient more than naive recursive one, but we can make it more faster and more easier to understand. Naive recursive and Memoized algorithm both calculate backwards, I mean Top to bottom. But as human being, we want to calculate bottom to top. Yes, it is more easier to understand. And somehow, when we calculate Fibonacci Number bottom to top. It's much effecient. We can make the space complexity O(1) but still the time complexity is O(n).

Here is the code.

```py
def fib_bottom_up_O1(n):

    if n <= 2: return 1

    prev, curr = 1, 1

    for k in range(2, n):
        prev, curr = curr, prev + curr

    return curr
```

It calculates bottom to up, n is used as the stop number in range().
We start calculate from index 2 in look but we don't use k. We just add up the current number and the previous number for each loop. Once it ends the loop, just return the current number.

In this code, we don't store any array but we just use prev and curr. So that the space complexity is 0(1).

## Bottom Up DP | Time complexity: O(n) / Space complexity: O(n)
Bottom Up DP with space complexity O(n) is nice. But with the code above, we only know the F(n) answer but not the every elements like 1,1,2,3,5 ... We can also figure it out with Bottom Up DP.

Here is the code.

```py
def fib_bottom_up_On(n):
    
    if n == 2: return [1, 1]
    if n == 1: return [1]
    
    fib = [0] * n
    fib[0], fib[1]  = 1, 1

    for k in range(2, n):
        fib[k] = fib[k - 1] + fib[k - 2]

    return fib
```

This function store each Fibonacci Number in loop. So that we can know the every Fibonacci Number in the range of nuber n. Althoug since it calculate every element, the space complexity is 0(n).

## Summarize
Dynamic Programming is the effiecnt way to solve the problem, but it is not noly one way, but many ways.
We have to choose the best way of DPs to solve the proble. It depends on what we want to figure it out.

And moreover, there are more ways to solve many problem with DPs.
- Dijkstra's algorithm for the shortest path problem
- A type of balanced 0–1 matrix
- And so on.

[Wikipedia: Dynamic programming](https://en.wikipedia.org/wiki/Dynamic_programming)

## How can this be applied to real-world problems?

## How does it compare with alternative approaches?

## When should I not use this algorithm?

## Reference
I studeid overview of Dynamic Programming with the YouTube video below.
Thanks to MIT for sharing the greate course online and free.
[YouTube: Lecture 19: Dynamic Programming I: Fibonacci, Shortest Paths](https://youtu.be/OQ5jsbhAv_M?si=TEhHy3YZJWpna8Eg)