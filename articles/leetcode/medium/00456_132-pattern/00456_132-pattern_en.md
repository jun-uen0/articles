## 456. 132 Pattern
URL: https://leetcode.com/problems/132-pattern   
Difficulty: Medium      

Even though the tag of this problem is "Binary Search",   
you can solve this problem without using binary search.   
However, it is a problem that can be solved by using a stack.   
But, although it can be expressed in a simple code, I could not solve it in the end.   
In order to be accepted, you need to implement it in O(N), but I could not reach that point.   
This time, I would like to explain based on the answer of [NeetCode](https://www.youtube.com/c/NeetCode)'s answer.   

Reference Code: [132 Pattern - Leetcode 456 - Python - YouTube](https://www.youtube.com/watch?v=q5ANAl8Z458&t)   

## Description
Given an array of n integers nums, a 132 pattern is a subsequence of three integers nums[i], nums[j] and nums[k]
such that i < j < k and nums[i] < nums[k] < nums[j].   

Return true if there is a 132 pattern in nums, otherwise, return false.   

## Code
```py
# To run this code localy,
# I changed the argument of the function to nums.
def find132pattern(nums):
  stack = []
  curMin = nums[0]
  for n in nums[1:]:
    while stack and n >= stack[-1][0]:
      stack.pop()
    if stack and n > stack[-1][1]:
      return True
    stack.append([n,curMin])
    curMin = min(curMin,n)
  return False
```

## Steps to solve
① Determine stack and minimum value with initial values   
② Create a for loop   
③ Store values in the stack   
④ Update the minimum value   
⑤ Take values out of the stack   
⑥ Check if 132 pattern exists   

## ① Determine stack and minimum value with initial values
stack:   
Make a stack to store values.   
The initial value is an empty list.   

curMin:   
Make a variable to store the current minimum value.   
The initial value is the first element of the array.   

```py
def find132pattern(nums):

  # Make variables
  stack = [] # Initialize stack with empty list
  curMin = nums[0] # Initialize curMin with the first element of the array
```

## ② Create a for loop
The range is from the second element of the array to the end.   
The reason why the range is from the second element of the array is because we have already stored the first element in curMin.   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  # Create a for loop
  for n in nums[1:]:
```

## ③ Store values in the stack
In the first loop, [2,1] is stored in stack,   
stack = [[2,1]]
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:

    # Store values in the stack
    stack.append([n,curMin])
```

## ④ Update current minimum value
Compare n and curMin just added to the stack,   
and update curMin to n if n is smaller.   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:
    stack.append([n,curMin])

    # Update current minimum value
    curMin = min(curMin,n)
```
## ⑤ Take values out of the stack
Compare n and the 0th element of the last element of the stack.   
If n is greater than or equal to the 0th element of the last element of the stack, take the value out of the stack.   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:

    # Take values out of the stack
    while stack and n >= stack[-1][0]:
      stack.pop()

    stack.append([n,curMin])
    curMin = min(curMin,n)
```
## ⑥ Check if 132 pattern exists
Finally, implement the 132 pattern judgment.   
Compare n and the 1st element of the last element of the stack.   
If n is greater than the 1st element of the last element of the stack, 132 pattern exists. Then return True.   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:
    while stack and n >= stack[-1][0]:
      stack.pop()

    # Check if 132 pattern exists
    if stack and n > stack[-1][1]:
      return True

    stack.append([n,curMin])
    curMin = min(curMin,n)
  return False
```
## Let's see the process of each loop
Let's say nums = [1,2,0,3,-1,6,3].   
Let's see the actual processing of each loop.   
The idea is to store the left value (minimum value of 132 pattern) and the middle value (maximum value of 132 pattern) in the stack for each loop, and judge it with the value of nums as the right value (intermediate value of 132 pattern).   

```py
nums = [1,2,0,3,-1,6,3]
  ...
  for n in nums[1:]:
  
    ## 1st loop
    # stack = [], curMin = 1, n = 2
    while stack and n >= stack[-1][0]: # False: stack is empty
      stack.pop()
    if stack and n > stack[-1][1]: # False: stack is empty
      return True
    stack.append([n,curMin]) # Update stack-> [[2,1]]
    curMin = min(curMin,n) # Update curMin -> 1
  
    ## 2nd loop
    # stack = [[2,1]], curMin = 1, n = 0
    while stack and n >= stack[-1][0]: # False: 0 >= 2
      stack.pop()
    if stack and n > stack[-1][1]: # False: 0 > 1
      return True
    stack.append([n,curMin]) # Update stack -> [[2,1],[0,1]]
    curMin = min(curMin,n) # Update curMin -> 0

    ## 3rd loop
    # stack = [[2,1],[0,1]], curMin = 0, n = 3
    while stack and n >= stack[-1][0]: # True: 3 >= 0 | True: 3 >= 2
      stack.pop() # Pop stack twice -> stack = []
    if stack and n > stack[-1][1]: # False: stack is empty
      return True
    stack.append([n,curMin]) # Update stack -> [[3,0]]
    curMin = min(curMin,n) # Update curMi -> 0

    ## 4th loop
    # stack = [[3,0]], curMin = 0, n = -1
    while stack and n >= stack[-1][0]: # False: -1 >= 3
      stack.pop()
    if stack and n > stack[-1][1]: # False: -1 > 0
      return True
    stack.append([n,curMin]) # Update stack -> [[3,0],[-1,0]]
    curMin = min(curMin,n) # Update curMin -> -1
  
    ## 5th loop
    # stack = [[3,0],[-1,0]], curMin = -1, n = 6
    while stack and n >= stack[-1][0]: # True: 6 >= -1 | True: 6 >= 3
      stack.pop() # Update stack / 2回pop() -> []
    if stack and n > stack[-1][1]: # False: stack is empty
      return True
    stack.append([n,curMin]) # Update stack -> [[6,-1]]
    curMin = min(curMin,n) # Update curMin -> -1
  
    ## 6th loop
    # stack = [[6,-1]], curMin = -1, n = 3
    while stack and n >= stack[-1][0]: # False: 3 >= 6
      stack.pop()
    if stack and n > stack[-1][1]: # True: 3 > -1
      return True # Found 132 pattern with [-1,6,3] / return True
    
  return False
```