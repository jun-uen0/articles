## 58. Length of Last Word
https://leetcode.com/problems/length-of-last-word   

Very easy problem.
You can try out your new programming language here.

## Problem
> Given a string `s` consisting of words and spaces, return *the length of the last word in the string.*  
A word is a maximal substring consisting of non-space characters only.

**Example**
```py
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```
## My solution
① split string s and add to list     
② return length of last element of list    

## Input
```py
print(s)
print(type(s))

# luffy   is still  joyboy
# <class 'str'>
```
## ① split string s and add to list 
```py
# Use `split()`, split string s by spaces,   
# and add to a list.
# No matter how many spaces exist between words, `split()` will work.

split_s = s.split()

# ['luffy', 'is', 'still', 'joyboy']
```

## ② return length of last element of list
```py
# Get last element of list you created at ①
# Get number of length of the last element

s.split()[-1] # joyboy
len(s.split()[-1]) # 6
```

## My answer
```
class Solution:
  def lengthOfLastWord(self, s: str) -> int:
    return len(s.split()[-1])
```