## Maximum Subarray

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
**Follow up:**

If you have figured out the *O(n)* solution, try coding another solution using the divide and conquer approach, which is more subtle.

**Code:**
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        s = 0
        max_sum = float('-inf')
        for n in nums:
            s += n
            max_sum = max(max_sum, s)
            if s < 0:
                s = 0
        return max_sum
```
We keep checking the current sum, if become negative, set it to zero, and we also keep track of the max. The reasoning behind this is, if you have left_sum, right_sum, as long as the left_sum is positive, it's always good to include them. Also, since every step, left is positive, so there's no break you can make there.