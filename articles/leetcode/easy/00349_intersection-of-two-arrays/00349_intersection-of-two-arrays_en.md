## 349. Intersection of Two Arrays
URL: https://leetcode.com/problems/intersection-of-two-arrays   
Difficulty: Easy

This is a simple and easy problem.
Although, I solved this problem using binary search, and a funciton that remove duplicates in list. My code is accepted but too long. I googled if someone wrote more short, readable, and efficient code. I found a code that is just one line. I realized how important it is to know the characteristics and rules of the programming language, syntax, and applications.

Reference: [[Java/Python 3] Slide Window O(n) codes]https://donic0211.medium.com/leetcode-349-intersection-of-two-arrays-9f99b27cf247)    

## Problem
Given two integer arrays nums1 and nums2, return an array of their intersection.   
Each element in the result must be unique and you may return the result in any order.   

## Examplesn
```py
Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
※ [4,9]でもOK
```

## Code
```py
def intersection(nums1, nums2):
  return list(set(nums1) & set(nums2))
```

## Step
① Remove duplicates from list
② Get the intersection of two sets
③ Convert to list

## ① Remove duplicates from list
Remove duplicates from list using set()
```py
nums1 = [4,9,5,4]
nums2 = [9,4,9,8,4]

def intersection(nums1, nums2):

  # Remove duplicates from list
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}
```

## ② Get the intersection of two sets
```py
def intersection(nums1, nums2):
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}

  # Get the intersection of two sets
  intersection = st_1 & st_2 # {4, 9}
```

## ③ Convert to list
```py
def intersection(nums1, nums2):
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}
  intersection = st_1 & st_2 # {4, 9}

  # Convert to list
  return list(intersection) # [4, 9]

  # If bundle the above three steps into one line
  return list(set(nums1) & set(nums2)) # [4, 9]
```

## Set()
[Python Remove Duplicates from a List - 2. set() function](https://www.digitalocean.com/community/tutorials/python-remove-duplicates-from-list)
Set() is a data type that does not allow duplicates.
Set does not have an order, so you cannot get elements using an index.
However, in this case, there is no need to get elements, so there is no problem.
## My solution
I place my solution below.
My code is too long.
In addition, it is slower than the code above.
I made a function to remove duplicates from a list, and a function to perform binary search.

```py
# Remove duplicates from list
def rm_d(lst):
  lst.sort()
  d = 0
  for i in range(1,len(lst)):
    if lst[i] == lst[i-1]:
      d+=1
    else:
      lst[i-d] = lst[i]
  return lst[0:len(lst)-d]

# Binary search
def bs(trgt,lst,r,l):
  while r <= l:
    m = (r+l)//2
    if lst[m] == trgt:
      return True
    elif lst[m] > trgt:
      l = m-1
      return bs(trgt,lst,r,l)
    else:
      r = m+1
      return bs(trgt,lst,r,l)
  return False
  

def intersection(nums1,nums2):

  # Merge sort both arrays
  # Eliminate duplicates from both arrays
  no_d_1 = rm_d(nums1)
  no_d_2 = rm_d(nums2)

  st = []

  # Iterate through shorter array and check if element is in longer array
  # If length of both is same, let's iterate nums1
  if len(no_d_1) <= len(no_d_2):
    for _,v in enumerate(no_d_1):

      # Binary search in no_d_2 with v
      # If found append v to st
      if bs(v,no_d_2,0,len(no_d_2)-1):
        st.append(v)

  else:
    for _,v in enumerate(no_d_2):
      if bs(v,no_d_1,0,len(no_d_1)-1):
        st.append(v)
  
  return st

# print(intersection(nums1,nums2))
```
