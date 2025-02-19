---

## **Greatest Common Divisor**
Let's implement an efficient function to compute the greatest common divisor using recursion in Python.  
The original code is borrowed from *Algorithm Science: A Beginner's Guide* by Tetsuo Asano, P.73.  
In this code, we use the **Euclidean algorithm** to calculate the greatest common divisor in **O(log n) divisions**.  

---

### **Code**
You can compute the greatest common divisor of two natural numbers, `m` and `n`, with the following code.  
If `n == 0`, `m` is returned as the greatest common divisor.  
If `n != 0`, the remainder of `m` divided by `n` is calculated, and the `gcd` function is called recursively.  

```py
def gcd(m, n):
    if n == 0:
        return m
    return gcd(n, m % n)
```

Since the greatest common divisor of `m` and `n` is the same as the greatest common divisor of `n` and `m % n`, the above code is valid.  
This method is known as the **Euclidean algorithm**.  

---

### **Processing Flow**
When you run the above code, the following steps will be executed:  

```py
gcd(12, 8) -> gcd(8, 4) -> gcd(4, 0) -> 4
```
The greatest common divisor of 12 and 8 is **4**.  

---

### **Euclidean Algorithm**
[Euclidean algorithm - Wikipedia](https://en.wikipedia.org/wiki/Euclidean_algorithm)  

This algorithm was already known in ancient Greece, but it was later named after **Euclid** when he included it in his book around **300 BC**.  
It is described in **Propositions 1 to 3 of Book 7 of *The Elements***.  
It is considered one of the oldest explicitly described algorithms.  