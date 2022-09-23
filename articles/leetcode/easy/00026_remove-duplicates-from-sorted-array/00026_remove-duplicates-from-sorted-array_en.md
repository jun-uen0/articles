## 26. Remove Duplicates from Sorted Array
https://leetcode.com/problems/remove-duplicates-from-sorted-array   
Difficulty: Easy

This is easy problem.   
Just remove duplicates from array. And the array is sorted.   
I will explain my code.   
※ You need to return the length of array k, not array itself.   
※ But you still have to operate array.   

## Description
Given an integer array nums sorted in non-decreasing order,   
remove the duplicates in-place such that each unique element appears only once.   
The relative order of the elements should be kept the same.   

Since it is impossible to change the length of the array in some languages,   
you must instead have the result be placed in the first part of the array nums.   
More formally, if there are k elements after removing the duplicates,   
then the first k elements of nums should hold the final result.   
It does not matter what you leave beyond the first k elements.   

**Return k** after placing the final result in the first k slots of nums.   

Do not allocate extra space for another array.   
You must do this by modifying the input array in-place with O(1) extra memory.   

## Solution
```python
# If you want to run this code on your local machine, you need to import List.
from typing import List
nums = [1,1,1,2,2,3,3,4] # Input

def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):
    if nums[i] == nums[i-1]:
      d+=1
    else:
      nums[i-d] = nums[i]
  return len(nums) - d
print(remove_duplicates(nums)) # 4
```
## Steps to solve
① Make a variable to count the duplicates of each element   
② Create a loop   
③ Check if the element is duplicated with the left element, and operate the array   
Let's see the array operation in detail   
④ Return the answer   

## ① Make a variable to count the duplicates of each element
Before executing the process in the loop,   
Prepare a variable to count the duplicates of each element.   

d... duplicate   
```py
def remove_duplicates(nums: List[int]):

  # Make a variable to count the duplicates of each element
  d = 0
```

## ② Create a loop
The range is all elements of array nums.
```py
def remove_duplicates(nums: List[int]):
  d = 0

  # Create a loop
  for i in range(1,len(nums)):
```

## ③ Check if the element is duplicated with the left element, and operate the array
Check if the element is duplicated with the left element.   
If it is duplicated, add 1 to the variable d that counts the duplicates.   
If it is not duplicated, shift the element to the left by the number of duplicates counted.   
```py
def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):

    # Check if the element is duplicated with the left element.
    ## If it is duplicated, add 1 to the variable d that counts the duplicates.
    if nums[i] == nums[i-1]:
      d+=1
    ## If it is not duplicated,
    ## shift the element to the left by the number of duplicates counted.
    else:
      nums[i-d] = nums[i]
```

## Let's see the array operation in detail
Let's say nums = [1,1,2,2,3,4]

```py
# 1st loop (i is nums[0]):
# d = 0
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 1 == undefined: False
  d+=1
else:
  nums[i-d] = nums[i] # nums[0-0] = nums[0] ※ No change in array

# 2nd loop (i is nums[1]):
# d = 0
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 1 == 1: True
  d+=1 # d = 1
else: # Skip
  nums[i-d] = nums[i]

# 3rd loop (i is nums[2]):
# d = 1
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 2 == 1: False
  d+=1
else:
  nums[i-d] = nums[i] # nums[2-1] = nums[2] ※ nums[1] = 2

# 4th loop (i is nums[3]):
# d = 1
# nums = [1,2,2,2,3,4]
if nums[i] == nums[i-1]: # 2 == 2: True
  d+=1 # d = 2
else: # Skip
  nums[i-d] = nums[i]

# 5th loop (i is nums[4]):
# d = 2
# nums = [1,2,2,2,3,4]
if nums[i] == nums[i-1]: # 3 == 2: False
  d+=1
else:
  nums[i-d] = nums[i] # nums[4-2] = nums[4] ※ nums[2] = 3

# 6th loop (i is nums[5]):
# d = 2
# nums = [1,2,3,2,3,4]
if nums[i] == nums[i-1]: # 4 == 3: False
  d+=1
else:
  nums[i-d] = nums[i] # nums[5-2] = nums[5] ※ nums[3] = 4

# After loop
# d = 2
# nums = [1,2,3,4,3,4]
```

## ④ Return the answer
Return the value of the length of the array minus the variable d that counts the duplicates.   
As mentioned at the beginning,   
In this answer, you need to return the number of elements you want to display.   
LeetCode will check the modified nums and determine whether it is correct or not.   

```py
def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):
    if nums[i] == nums[i-1]:
      d+=1
    else:
      nums[i-d] = nums[i]

  # Return the answer
  return len(nums) - d
```