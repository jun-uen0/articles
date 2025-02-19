## Finding Perfect Numbers in Python

The following Python code finds perfect numbers within a given range:

```py
def is_perfect(n):
    divisors = [i for i in range(1, n) if n % i == 0]
    return sum(divisors) == n

# Find perfect numbers up to 10000
for num in range(1, 10001):
    if is_perfect(num):
        print(num)
```

Running this code will output perfect numbers such as 6, 28, 496, and 8128.

---

## Efficient Perfect Number Checking Using Mersenne Primes

Using Mersenne primes, we can efficiently determine whether a number is perfect. The following Python code checks if a given number is a perfect number:

```py
def is_mersenne_prime(num):
    if num <= 1:
        return False
    if num == 2:
        return True
    if num % 2 == 0:
        return False
    
    for i in range(3, int(num ** 0.5) + 1, 2):
        if num % i == 0:
            return False
    return True

def check_perfect_number(num):
    if num % 2 != 0:
        return False
    
    n = 1
    while (1 << n) - 1 <= num:
        if (1 << (n - 1)) * ((1 << n) - 1) == num:
            if is_mersenne_prime((1 << n) - 1):
                return True
        n += 1
    
    return False

# Find perfect numbers up to 10000
for num in range(1, 10001):
    if check_perfect_number(num):
        print(num)
```

This code optimizes the calculation of perfect numbers using Mersenne primes.

---

## References

- [Perfect number - Wikipedia](https://en.wikipedia.org/wiki/Perfect_number