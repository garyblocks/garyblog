# Two Sum II - Input array is sorted

Given an array of integers that is already *sorted in ascending order*, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

**Note:**

* Your returned answers (both index1 and index2) are not zero-based.
* You may assume that each input would have exactly one solution and you may not use the same element twice.

**Example:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.
```

**Code:**

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, h = 0, len(numbers) - 1
        while l <= h:
            if numbers[l] + numbers[h] == target:
                return [l+1, h+1]
            elif numbers[l] + numbers[h] > target:
                h -= 1
            else:
                l += 1
```
Not a big difference from the original two sum. We can use two pointer to achieve O(N) when the array is sorted.