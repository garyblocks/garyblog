# Maximum Product Subarray

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example:**
```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

**Code:**

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        maxp = -10000
        cur_min, cur_max = 10000, -10000
        for n in nums:
            if n < 0:
                cur_min, cur_max = cur_max, cur_min
            cur_max = max(cur_max * n, n)
            cur_min = min(cur_min * n, n)
            maxp = max(maxp, cur_max)
        return maxp
```
keep two lists max and min, when the number is negative, swap them.
