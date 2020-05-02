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
We keep checking the current sum, if it becomes negative, set it to zero, and we also keep track of the max. 

array:  l l l l | r r r r
The reasoning behind this is, if you have left sum and right sum, as long as the left sum is positive, it's always better to include them.
But inside the left subarray, is it possible to get a bigger sum? The only way to get an unchecked bigger sum is the s part:

array: l l s s | r r r r

if ss is bigger than llss, then ll would be negative, they will be dropped. 
