## 69. Sqrt(x) 
https://leetcode.com/problems/sqrtx

My answer was O(n), so the execution time was too long.   
To reduce the time complexity to O(logn), I will explain the solution using binary search.   
I want to improve my skill so that I can explain my answer someday.   


Reference Code: [Python binary search solution (O(lgn))](https://leetcode.com/problems/sqrtx/discuss/25061/Python-binary-search-solution-(O(lgn)))

## Description
Given a non-negative integer x,   
compute and return the square root of x.   

Since the return type is an integer,   
the decimal digits are truncated,   
and only the integer part of the result is returned.   

**Example**
```py
Example 1:
Input: x = 4
Output: 2

Example 2:
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
```

## Solution
Time complexity: O(LogN)   
```py
# Input
x = 10

def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    else:
      l = mid + 1

print(sqrtx(x)) # 3
```

## ① Make variables
l... left end value
r... right end value
```py
# Define function sqrtx with argument x
def sqrtx(x):
  # Make variables l and r
  l, r = 0, x
```

## ② Make a loop
in this process, left end and right end values are updated in the loop process.   
With each loop, left end and right end values are approaching the center value.   
In the worst case, left end and right end values are the center value (the same value).   
```py
def sqrtx(x):
  l, r = 0, x

  # Make a loop
  while l <= r:
```

## ③ Calculate the middle value of l and r
In this case, l=0, r=10,    
mid = 0 + (10-0)//2 = 5   
※ 「//」 is floor division (9//2 = 4)   

```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:

    # Calculate the middle value of l and r
    mid = l + (r-l)//2
```

## ④ (Base case) return the square root of x, or its approximate value
Return mid if square value of mid is less than x and square value of mid+1 is greater than or equal to x.   
In this case, mid is the answer of the problem, so return mid.   

The reason why you can get the square root of 10 by this calculation is that,   
for example, if x is 10 and mid is 3, the condition expression of if statement is "9 (3 * 3) <= 10 <16 (4 * 4)".   
The square root of 10 is 3.1622776601683795,   
and the integer part of 3.1622776601683795 is 3, so return the value of mid, which is 3.   

Place this base case at the beginning of the loop process.   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2

    # Return the square root of x, or its approximate value
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
```

## ⑤ Exclude the right side of the search range
If x is less than the square of mid,   
for example, if x is 10 and mid is 5, 10 < 25 (5 * 5)   
Set the right end (r) to 4 (5-1).   
The calculation range becomes 0~4 in the next loop.   

```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    
    # Exclude the right side of the search range
    elif x < mid * mid:
      r = mid - 1
```
## ⑥ Exclude the left side of the search rangen
If x is greater than or equal to the square of mid,   
for example, if x is 10 and mid is 3, 9 (3 * 3) <= 10   
Set the left end (l) to 4 (3+1).   
The calculation range becomes 4~10 in the next loop.   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    
    # Exclude the left side of the search rangen
    else:
      l = mid + 1
```

## ⑦ Output the result
```py
# Input
x = 10

def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    else:
      l = mid + 1

print(sqrtx(x)) # 3
```