## 3. Longest Substring Without Repeating Characters
URL: https://leetcode.com/problems/longest-substring-without-repeating-characters
Difficulty: Medium

## Problem Statement
Given a string, find the length of the longest substring without repeating characters.

## Example
```py
例1
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

例2
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

例3
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## My Answer
```py
# s = 'pwawkew'
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1
  
  cnt = 0
  tmp = [s[0]]

  for i in range(1,len(s)):
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])
    if len(tmp) > cnt:
      cnt = len(tmp)
  return cnt

print(lengthOfLongestSubstring(s))
```

## ① Base Case
Return 0 if the length of the string is 0.
Return 1 if the length of the string is 1.
```py
def lengthOfLongestSubstring(s: str):

  # Base Case
  if len(s) == 0: return 0
  if len(s) == 1: return 1
```

## ② Make substring in each loop
```py
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1

  # Initialize tmp with the first element of s
  tmp = [s[0]]

  for i in range(1,len(s)):

    # If tmp = [p,w,a,k] and s[i] = w,
    # slice tmp from the next element of the index of w (2)
    # tmp = [a] and tmp = [a,w] in the next loop
    # So, we can make a substring without duplication in each loop
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])
```

## ③ Count the length of the longest substring
We can make a substring without duplication in each loop.
Next, count the length of the substring in each loop.
```py
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1
  tmp = [s[0]]

  # Initialize cnt with 0
  cnt = 0

  for i in range(1,len(s)):
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])

    # If the length of tmp is longer than cnt,
    # update cnt to the length of tmp
    if len(tmp) > cnt:
      cnt = len(tmp)
      
  # Return the length of the longest substring
  return cnt
```
