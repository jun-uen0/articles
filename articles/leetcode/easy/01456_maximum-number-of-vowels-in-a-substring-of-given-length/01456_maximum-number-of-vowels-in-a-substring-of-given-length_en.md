## 1456. Maximum Number of Vowels in a Substring of Given Length
 https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length   

## Reference
Code: [[Java/Python 3] Slide Window O(n) codes](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/discuss/648559/JavaPython-3-Slide-Window-O(n)-codes)   
User: [rock](https://leetcode.com/rock)  

## Description
Given a string s and an integer k,  
return the maximum number of vowel letters in any substring of s with length k.   
Vowel letters in English are 'a', 'e', 'i', 'o', and 'u'.    

**Example**
```py

Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
#「abc」「bci」「cii」「iii」「iid」「def」

Input: s = "aeiou", k = 2
Output: 2
Explanation: Any substring of length 2 contains 2 vowels.
#「ae」「ei」「io」「ou」

Input: s = "leetcode", k = 3
Output: 2
Explanation: "lee", "eet" and "ode" contain 2 vowels.
# 「lee」「eet」「etc」「tco」「cod」「ode」
```

## Solution
```py
# Input
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0
for i, v in enumerate(s):
  if v in vowels:
    cnt += 1
  if i >= k and s[i-k] in vowels:
    cnt -= 1
  ans = max(cnt, ans)
print(ans) # 3
```

## ① Provide variables
`vowels` contains vowels in dectionary   
`ans` and `cnt` with initial value 0   
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0
```

## ② Make for loop
We use `enumerate()` to use index and value of string s   
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):
  # Here is some code
print(ans) # answer with ans
```

## ③ Count up with 1 when find vowel in string s
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # Count up
  if v in vowels:
    cnt += 1

print(ans)
```

## ④ Avoid too much counting
We need to avoid too much counting.
For example if input s is 'abciiidef', we find two vowels in 4th loop. ("a" and "i")   
But we shoud not count index of 0, which value is a.
Becouse in 4th loop, the substring is "bci".
Thus we need to **count down with 1** for index of 0, "a".

We need to check the index of `s[i-k]` when `i` is equal to or larger than k.


```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # Count up
  if v in vowels:
    cnt += 1
  
  # Count down
  if i >= k and s[i-k] in vowels:
    cnt -= 1

print(ans)
```

## ⑤ Substitute max value of `ans` and `cnt` in every loop

In every for loop, we substitute max number of `ans` and `cnt` to `ans`   
Number of `cnt` is dynamic. Its value changes in every loop     
Therefore we need to get max value of `ans` and `cnt` in every loop   
And then substitute it to `ans`  

```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # Count up
  if v in vowels:
    cnt += 1
  
  # Count down
  if i >= k and s[i-k] in vowels:
    cnt -= 1
  
  # Get max value
  ans = max(cnt, ans)

print(ans)
```