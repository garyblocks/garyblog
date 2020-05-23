## 3Sum
Given an array `nums` of n integers, are there elements a, b, c in `nums` such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is: [ [-1, 0, 1],
  [-1, -1, 2]
]
```
**Code:**

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ret = []
        N = len(nums)
        if N < 3:
            return ret
        nums = sorted(nums)
        for i, n in enumerate(nums[:-2]):
            if n > 0:
                break
            if i > 0 and n == nums[i-1]:
                continue
            l, h = i+1, N - 1
            while l < h:
                if n + nums[l] + nums[h] < 0:
                    l += 1
                elif n + nums[l] + nums[h] > 0:
                    h -= 1
                else:
                    ret.append([n, nums[l], nums[h]])
                    while l < h and nums[l] == nums[l+1]: l += 1
                    while l > h and nums[h] == nums[h-1]: h -= 1
                    l += 1
                    h -= 1
        return ret
```
First we sort the list then do a for loop for the first number. Then we are down to find the sum for two numbers that equals minus first number. 

To find all the combinations, we can have two pointers, moving towards each other, if the sum is larger than we need, we can reduce the right pointer, so we have a smaller number and vice versa. In the meantime, we are skipping all the numbers we have seen, so we don't have duplicates in the return list.

