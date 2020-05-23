# Kth Largest Element in an Array

Find the *k*th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```
```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:**
You may assume k is always valid, 1 ≤ k ≤ array's length.

**Code:**

```python
from random import randint
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        def select(i, j):
            if i == j:
                return i, nums[i]
            pi = randint(i, j) 
            nums[pi], nums[j] = nums[j], nums[pi]
            pivot = nums[j]
            right = i
            for left in range(i, j):
                if nums[left] < pivot:
                    nums[left], nums[right] = nums[right], nums[left]
                    right += 1
            nums[j], nums[right] = nums[right], nums[j]
            return right, pivot
        
        low, high = 0, len(nums) - 1
        k = len(nums) - k + 1
        while True:
            pi, p = select(low, high)
            if pi == k-1:
                return p
            elif pi < k-1:
                low = pi + 1
            else:
                high = pi - 1
```
Use quick sort to find the recursively find the kth biggest element.