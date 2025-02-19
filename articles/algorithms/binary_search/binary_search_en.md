
## Binary Search (English)
Binary search is an algorithm to check if a target number exists in a list.
The time complexity of this algorithm is O(log N).

```py
# Is the number "5" in the list?
trgt = 5
lst = [1, 2, 5, 8, 12, 19, 34]
```

## Prerequisites
- The list elements must be numbers.
- The list must be sorted.

## Process
1. Get the middle value of the list.
2. Compare the target number with the obtained value.
3. Based on the comparison:
   - If they match, return the index.
   - If the target is greater, continue searching in the right half.
   - If the target is smaller, continue searching in the left half.
4. If the target number is not found, return None.

## Example Calculation
```py
trgt = 5
lst = [1, 2, 5, 8, 12, 19, 34]
mid = len(lst) // 2  # 3
mid_n = lst[mid]  # 8
```
Since 5 is smaller than 8, search the left half `[1, 2, 5]`.

```py
mid = len(lst) // 2  # 1
mid_n = lst[mid]  # 2
```
Since 5 is greater than 2, search the right half `[5]`.

## Iterative Implementation
```py
def binary_search_itr(lst, target):
    start = 0
    end = len(lst) - 1
    while start <= end:
        mid = (start + end) // 2
        if lst[mid] == target:
            return mid
        if lst[mid] > target:
            end = mid - 1
        else:
            start = mid + 1
    return None
```

## Recursive Implementation
```py
def binary_search_rcr(lst, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    if lst[mid] == target:
        return mid
    elif lst[mid] > target:
        return binary_search_rcr(lst, target, start, mid - 1)
    else:
        return binary_search_rcr(lst, target, mid + 1, end)
```