# Next Permutation

mplement *next permutation*, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

**Code:**

```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        if len(nums) < 2:
            return nums
        # find the first decresing digit from the end
        left = -1
        for i in range(len(nums)-2, -1, -1):
            if nums[i] < nums[i+1]:
                left = i
                break
        if left < 0:
            nums[:] = nums[::-1]
            return
        # find first bigger digit
        m = float('inf')
        right = i
        for j in range(i+1, len(nums)):
            if nums[j] > nums[left] and nums[j] < m:
                m = nums[j]
                right = j
        # swap
        nums[right], nums[left] = nums[left], nums[right]
        # reorder
        nums[left+1:] = sorted(nums[left+1:])
        return
```
Follow the steps.
