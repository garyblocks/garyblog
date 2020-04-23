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
        l, h = 0, len(nums) - 1
        while l <= h:
            m = (l + h) // 2
            if nums[m] == target:
                return m
            elif nums[m] >= nums[l]:
                if nums[l] <= target <= nums[m]:
                    h = m - 1
                else:
                    l = m + 1
            else:
                if nums[m] <= target <= nums[h]:
                    l = m + 1
                else:
                    h = m - 1
        return -1
```
Modify the binary search to check if the mid point is before the pivot or after pivot.