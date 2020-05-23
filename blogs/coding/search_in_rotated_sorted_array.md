## Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O(log n)*.

**Example:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

**Code:**

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
            
        l, h = 0, len(nums)-1
        while l + 1 < h:
            m = (l + h) // 2
            mid = nums[m]
            if mid == target:
                return m
            elif mid > target:
                if target < nums[0] and mid >= nums[0]:
                    l = m
                else:
                    h = m
            else:
                if target >=  nums[0] and mid < nums[0]:
                    h = m
                else:
                    l = m
                    
        if nums[l] == target:
            return l
        elif nums[h] == target:
            return h
        else:
            return -1
```
Use the binary search template, there's only one condition that the binary search need to do different thing, that is when target and mid point are in different parts.