## Product of Array Except Self
Given an array `nums` of n integers where n > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of nums except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
Constraint: It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.
```
**Note:** Please solve it without division and in O(n).

**Follow up:**
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

**Code:**

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        N = len(nums)
        # build left and save in the return values
        ret = [1] * N
        for i in range(1, N):
            ret[i] = nums[i-1] * ret[i-1]
        
        # put right in when reverse tranverse the array
        right = 1
        for i in reversed(range(N)):
            ret[i] *= right
            right *= nums[i]
        
        return ret
```
Idea: use the product of left and right

We start by building the products from two directions: left and right. When there's no number on the left or right, we default to 1.

For the right products, we only need to keep a single variable, and update the value when looping through the array from the right end.

Time complexity is O(N),
Space complexity is O(1).