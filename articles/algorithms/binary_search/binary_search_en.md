## Binary Search
You can check if target number is in the list.    
You can do it in O(logN).    

```py
# Is the number "5" in the list?

trgt = 5
lst = [1,2,5,8,12,19,34]
```

## Prerequisites
The elements in the list are number type.   
The list is merged.    

## Proccess
① Get the number in the middle of the list, (or one to the left of the center).    
② Compare the target number and the number obtained.    
③-① If the result is the same, return the element number.   
③-② If the result is that the target number is larger than the number obtained, start the process from ① again in the right side of the list divided by the middle value.
③-③ If the result is that the target number is smaller than the number obtained, start the process from ① again in the left side of the list divided by the middle value.
④ If the target number is not in the list, return None.  

## ① Get the number in the middle of the list, (or one to the left of the center).

```py
trgt = 5
lst = [1,2,5,8,12,19,34]

mid = len(lst) // 2 # 3
mid_n = lst[mid] # 8
```

## ② Compare the target number and the number obtained.
The target value is 5
The center value is 8
-> The target number is smaller than the number obtained.

## ③-① If the result is the same, return the element number.
The result of ② is that the target number is smaller than the number obtained.   
So, divide the list by the middle value and start the process from ① again in the left side of the list.   

```py
# update lst with left side of the list divided by the middle value.
lst = lst[:mid] # [1,2,5]
```

## (2nd time) ① Get the number in the middle of the list, (or one to the left of the center).
```py
# trgt = 5
# lst = [1,2,5]

mid = len(lst) // 2 # 1
mid_n = lst[mid] # 2
```

## (2nd time) ② Compare the target number and the number obtained.
The target value is 5   
The center value is 2   
-> The target number is larger than the number obtained.    

## (2nd time) ③-② If the result is that the target number is larger than the number obtained, start the process from ① again in the right side of the list divided by the middle value.
The result of ② is that the target number is larger than the number obtained.
So, divide the list by the middle value and start the process from ① again in the right side of the list.

```py
# update lst with right side of the list divided by the middle value.
lst = lst[(mid+1):] # [5]
```

## (3rd time) ① Get the number in the middle of the list, (or one to the left of the center).
```py
# trgt = 5
# lst = [5]

mid = len(lst) // 2 # 0
mid_n = lst[mid] # 5
```
## (3rd time) ② Compare the target number and the number obtained.
The target value is 5   
The center value is 5   
-> The result is the same.

## About processing times
The target number was found in 3 processes.   
If the list has only a few elements, there is not much difference.    
But if the list has 10 million elements, you can find the target number in 24 processes.    
```py
(1回) 10000000
(2回) 5000000
(3回) 2500000
(4回) 1250000
(5回) 625000
(6回) 312500
(7回) 156250
(8回) 78125
(9回) 39062
(10回) 19531
(11回) 9765
(12回) 4882
(13回) 2441
(14回) 1220
(15回) 610
(16回) 305
(17回) 152
(18回) 76
(19回) 38
(20回) 19
(21回) 10
(22回) 5
(23回) 2
(24回) 1
```  
The list of search targets is halved each time the process is passed.   
The number of searches is O(Log N).   

## Code with iterative method
```py
def binary_search_itr(lst, target):
  start = 0
  end = len(lst) - 1

  # Loop until list is empty
  while start <= end:
    mid = (start + end) // 2
    # If target and middle value are same, return element number
    if lst[mid] == target:
      return mid
    # If target is larger than middle value, move to search on right side of list
    if lst[mid] > target:
      end = mid - 1 # update end
    # If target is smaller than middle value, move to search on left side of list
    else:
      start = mid + 1　# update start
  
  # If target is not in the list, return None
  return None

my_list = [1, 3, 5, 7, 9]
print(binary_search_itr(my_list, 3))  # 1
print(binary_search_itr(my_list, -1)) # None
```

## Code with recursive method
```py
def binary_search_rcr(lst, target, start, end):
  # Loop until list is empty
	while start <= end:
		mid = (end + start) // 2

    # If target and middle value are same, return element number
		if lst[mid] == target:
			return mid

    # If target is larger than middle value, move to search on right side of list
		elif lst[mid] > target:
			end = mid - 1
      # Call this function recursively
			return binary_search_rcr(lst, target, start, end)
    
    # If target is smaller than middle value, move to search on left side of list
		else:
			start = mid + 1
      # Call this function recursively
			return binary_search_rcr(lst, target, start, end)
  
  # If target is not in the list, return None
	return None

my_list = [1, 3, 5, 7, 9]
print(binary_search_rcr(my_list, 9, 0, len(my_list)-1)) # 4
print(binary_search_rcr(my_list, 10, 0, len(my_list)-1)) # None
```
