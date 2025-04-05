# Dynamic Programming: Longest Increasing Subsequence (LIS)

## Problem
Given an integer array, return the length of the longest strictly increasing subsequence.

## Tabulation (O(n^2))
```python
def lengthOfLIS(nums):
    n = len(nums)
    dp = [1] * n
    for i in range(n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)
```
