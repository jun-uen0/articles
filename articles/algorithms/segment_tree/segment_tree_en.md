# Segment Tree
## Introduction
Segment Tree is an efficient tree data structure for dynamic range queries.
That is the reason why its name is "Segment" Tree.
The arrary is recursively diveided into two segments until the segment size is 1.
The concept of dividing into segments sounds like binary search method.
Trade-offs: It uses many memory.

## How to implement
Example: finding the maximum value of range
```py
class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.tree_size = 1
        self.init_value = float("-inf")

        while self.tree_size < self.n:
            self.tree_size *= 2

        # Create the data set
        # Space complexity: 0(2n)
        self.data = [self.init_value] * (2 * self.tree_size)

        # Build the segment tree
        # Time complexity: O(n)
        for i in range(self.n):
            self.data[self.tree_size + i] = arr[i]
        
        # Time complexity: O(n)
        for i in range(self.tree_size - 1, 0, -1):
            self.data[i] = max(self.data[i * 2], self.data[i * 2 + 1])

    def update_node(self, index, value):
        node = index - 1 + self.tree_size
        self.data[node] = value

        # Time complexity: O(log n)
        while node > 1:
            parent = node // 2
            self.data[parent] = max(self.data[parent * 2], self.data[parent * 2 + 1])
            node = parent

    def range_max(self, left, right):

        # Base case: left must be smaller than right
        if left > right:
            return float("-inf")
        
        left += self.tree_size - 1
        right += self.tree_size - 1
        res = float("-inf")
        
        # Time complexity: O(log n)
        while left <= right:
            if left % 2 == 1:
                res = max(res, self.data[left])
                left += 1
            if right % 2 == 0:
                res = max(res, self.data[right])
                right -= 1
            left //= 2
            right //= 2
        
        return res


# Example usage:
arr = [1, 2, 3, 4, 5, 6, 7]
seg_tree = SegmentTree(arr)

# Update values
seg_tree.update_node(1, 2)
seg_tree.update_node(2, 4)
seg_tree.update_node(3, 1)
seg_tree.update_node(4, 5)
seg_tree.update_node(5, 4)
seg_tree.update_node(6, 3)
seg_tree.update_node(7, 2)

# Querying segment tree
print(seg_tree.range_max(6, 2))  # Invalid range -> returns -inf
print(seg_tree.range_max(2, 2))  # Should return 4
print(seg_tree.range_max(3, 7))  # Should return 5

```
## When should it be used
- When we want to need answer of range queries with efficient way
- And also, update the element dynamically

## How can this be applied to real-world problems?
- Stock market analysis
- Big data queries

## How does it compare with alternative approaches?
Segment Tree vs. Fenwick Tree:
- Fenwick Tree is more simple. But it doesn't support dynamic updating.

Segment Tree vs. Sparse Table:
- Sparse Table is faster than Segement Tree. 0(1) vs. 0(log n)
- But Sparse Table support only static arrays.

## When should I not use this algorithm?
- Since Segment Tree use 0(2n) space complexity, I should not use it if I don't have memory enough.
- If the element is not updated frequently, we should use the built-in method like max(). max() use only 0(n) space complexity.


# AVL Tree

# Applications (Real-World Use Cases)
## How can this be applied to real-world problems?
## How does it compare with alternative approaches?
## When should I not use this algorithm?