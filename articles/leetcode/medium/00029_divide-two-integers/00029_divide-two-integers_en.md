## 29. Divide Two Integers
https://leetcode.com/problems/divide-two-integers   
Difficulty: **Medium**     

In this article, I will explain how to solve the problem [Divide Two Integers](https://leetcode.com/problems/divide-two-integers) with [Timothy H Chang](https://www.youtube.com/user/timc3406)'s solution. His solution is best one I've ever seen, very simple and easy to understand.
Timothy H Chang's solution: [Leetcode - Divide Two Integers (Python)](https://www.youtube.com/watch?v=6kFp_s_UtPE)      

## Problem Description
Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.   

The integer division should truncate toward zero, which means losing its fractional part. For example, 8.345 would be truncated to 8, and -2.7335 would be truncated to -2.   

Return the quotient after dividing dividend by divisor.   

Note: Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For this problem, if the quotient is strictly greater than 231 - 1, then return 231 - 1, and if the quotient is strictly less than -231, then return -231..       

**Example**
```py
# Example 1:
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = truncate(3.33333..) = 3.

# Example 2:
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = truncate(-2.33333..) = -2.
```

## Solution
Time complexity: O(logn)
```py
# Input
dividend = 10
divisor = -10

def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      output += mul
      mul += mul
      temp += temp

  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
  
  return min(2147483647,max(-21474836478, output))

print(divide_faster()) # -3
```

## Steps to solve
① Set basic case   
② Get the absolute value of dividend and divisor   
③ Create a loop to process while dividend's absolute value   
    can be divided by divisor's absolute value   
③-① Create two variables for calculation in the loop   
④ Create a loop to process while dividend's absolute value is greater than or equal to temp   
④-① Subtract the divisor from the dividend in the loop   
⑤ Investigate the loop process in ③   
⑥ Determine the sign of output by conditional expression   
⑦ Return the final answer   

## ① Set basic case   
If dividend is 0, return 0.   
```py
def divide_faster() -> int:

  # Basic case
  if dividend == 0:
    return 0
```

## ② Get the absolute value of dividend and divisor
Calculate with the absolute value of each. Because we need to handle negative numbers.   
First, calculate with integers.   
If dividend or divisor is a negative number, convert the output to a negative number at the end.   

```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  # Get the absolute value of dividend and divisor
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)

  # Initialize output
  output = 0
```


## ③ Create a loop to process while dividend's absolute value can be divided by divisor's absolute value
If dividend's absolute value is greater than or equal to divisor's absolute value,   
it means that dividend's absolute value can be divided by divisor's absolute value.   


```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  # Create a loop to process while dividend's absolute value
  # can be divided by divisor's absolute value
  while dividend_abs >= divisor_abs:
```

## ③-① Create two variables for calculation in the loop
temp:
Initialize with divisor_abs.
This value will increase exponentially in the next loop.

mul:
Initialize with 1.
This value will increase exponentially in the next loop.
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    # Create two variables for calculation in the loop
    temp = divisor_abs # Assign divisor_abs to temp
    mul = 1 # Assign mul to quotient
```

## ④ Create a loop to process while dividend's absolute value is greater than or equal to temp
In this proccess the divisor is temp,
and the dividend is dividend_abs.   
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1

    # Create a loop to process while dividend's absolute value is
    # greater than or equal to temp
    while dividend_abs >= temp:
```

## ④-① Update the variables used in the process of ⑤ 
dividend_abs:
If dividend_abs is greater than or equal to temp, subtract temp from dividend_abs.

output:
output is the final answer.
Its initial value is 0, and the value of mul is added each time the loop is repeated.

mul:
Each loop, the value of mul is doubled.

temp:
Each loop, the value of temp is doubled.

```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1

    while dividend_abs >= temp:

      # Update the variables used in the process of ⑤
      dividend_abs -= temp # Subtract temp from dividend_abs
      output += mul # Add mul to output
      mul += mul # Double the value of mul
      temp += temp # Double the value of temp
```

## How the loop proccessing in ③ works
For example, let's assume that dividend_abs is 100 and divisor_abs is 3.   
```py
dividend_abs = 10
divisor_abs = 3

while dividend_abs >= divisor_abs: # 100 >= 3
  temp = divisor_abs # temp = 3
  mul = 1

  # Loop 1 (while dividend_abs >= temp: # 100 >= 3)
    dividend_abs -= temp # 100 - 3 = 97
    output += mul # 0 + 1 = 1
    mul += mul # 1 + 1 = 2
    temp += temp # 3 + 3 = 6

  # Loop 2 (while dividend_abs >= temp: # 97 >= 6)
    dividend_abs -= temp # 97 - 6 = 91
    output += mul # 1 + 2 = 3
    mul += mul # 2 + 2 = 4
    temp += temp # 6 + 6 = 12
  
  # Loop 3 (while dividend_abs >= temp: # 91 >= 12)
    dividend_abs -= temp # 91 - 12 = 79
    output += mul # 3 + 4 = 7
    mul += mul # 4 + 4 = 8
    temp += temp # 12 + 12 = 24
  
  # Loop 4 (while dividend_abs >= temp: # 79 >= 24)
    dividend_abs -= temp # 79 - 24 = 55
    output += mul # 7 + 8 = 15
    mul += mul # 8 + 8 = 16
    temp += temp # 24 + 24 = 48
  
  # Loop 5 (while dividend_abs >= temp: # 55 >= 48)
    dividend_abs -= temp # 55 - 48 = 7
    output += mul # 15 + 16 = 31
    mul += mul # 16 + 16 = 32
    temp += temp # 48 + 48 = 96
  
  # Loop 6 (while dividend_abs >= temp: # 7 >= 96)
    # Since it does not match the condition expression, it will exit the loop.
    # The current output value is 31.
    # Therefore, the answer when dividend_abs is 100 and divisor_abs is 3 is 31.
```
The reason this process is fast is because it does not subtract 100 from 3 every time,   
but instead increases the divisor by 2 each time the process is repeated.   
If this calculation were 100/3, the number of processes would be 100/3=33 times.   
However, as shown in the example above, if this method is used, the number of processes will be just 6 times.   

## ⑥ Convert the sign of output to positive or negative  
If dividend is negative, and divisor is positive, OR   
If dividend is positive, and divisor is negative,   
Convert the sign of output to negative.   
```py
def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      
      output += mul
      mul += mul
      temp += temp

  # Convert the sign of output to positive or negative
  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
```

## ⑦ Return the final answer
In normal cases, return the value of output.   
However, if the value of output exceeds the range of 32-bit integers,   
return the maximum value of 32-bit integers (2^31 - 1).   
```py
def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      
      output += mul
      mul += mul
      temp += temp

  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
  
  # Return the final answer
  return min(2147483647,max(-21474836478, output))
```