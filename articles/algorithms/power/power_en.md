## Exponential function
Let's implement an efficient power function using recursion in Python.
The original code is borrowed from "Algorithm Science: Introduction to Super Introduction" by Shigehiro Asano, P.70.

## Full Code
You can compute the power efficiently by using the following code.
For example, if you calculate x^13, the number of executions is 4.
```py
def power(x,k):
  if k == 1:
    return x
  m = k//2 # floor
  t = power(x,m) # calculate recursively
  if k % 2 == 0:
    return t * t
  else:
    return t * t * x
```

## Processing flow
When you actually execute the above code, the following processing flow will occur.
power(x,13) -> power(x,6) -> power(x,3) -> power(x,1)
x^13 is equivalent to x^6*x
x^6 is equivalent to x^3*
x^3 is equivalent to x^1*x
x^1 is equivalent to x