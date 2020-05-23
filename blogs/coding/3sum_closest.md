## 3Sum Closest
Given an array `nums` of n integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```
**Code:**

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        delta = float('inf')
        nums = sorted(nums)
        for i, n in enumerate(nums[:-2]):
            l, h = i+1, len(nums) - 1
            while l < h:
                s = nums[l] + nums[h] + n
                if s == target:
                    return s
                if abs(s - target) < abs(delta):
                    delta = s - target
                if s < target:
                    l += 1
                else:
                    h -= 1
        return target + delta
```
The idea is the same as 3Sum, sort the array first, then fix one number and search for the other two. Keep a delta to record the minimal difference from the target. Do a check every time to cover all differences.