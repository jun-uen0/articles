## Greatest Common Divisor
Let's implement an efficient power function using recursion in Python.   
The original code is borrowed from "Algorithm Science: Introduction to Super Introduction" by Shigehiro Asano, P.73.   
In this code, we use the Euclidean algorithm to calculate the greatest common divisor in O(log n) times of division.   

## Code
You can compute the greatest common divisor of m and n, two natural numbers, with the following code.   
If n is 0, m is returned as the greatest common divisor.   
If n is not 0, the remainder of m divided by n is calculated, and the gcd function is called recursively.   

```py
gcd(m,n):
 if n == 0: return m
 return gcd(m,m%n)
```
## Processing flow
When you actually execute the above code, the following processing flow will occur.   
gcd(12,8) -> gcd(8,4) -> gcd(4,0) -> 4   
The greatest common divisor of 12 and 8 is 4.   

## Euclidean algorithm
[Euclidean algorithm - Wikipedia](https://en.wikipedia.org/wiki/Euclidean_algorithm)
The algorithm was known among the clever ancient Greeks, but it became known as Euclid's name when he was written in his book around 300 BC.   
It is described in Proposition 1 to 3 of Volume 7 of the "Original".   
It is called the oldest algorithm explicitly described.   
