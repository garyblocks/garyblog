## Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

**Code:**

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # build a hash map from number to index
        hash_map = {
            n: i for i, n in enumerate(nums)
        }
        
        # loop the nums, see if a num exists in hash_map
        # and have a different index
        for i, n in enumerate(nums):
            if target - n in hash_map and i != hash_map[target - n]:
                return [i, hash_map[target - n]]
```
The idea here is to create a hash map saving all the number's index, and then loop the number list again, to find if the difference between each number and the target exists in the hashmap.

The reason to use hash map here is to have O(1) search time for a value, a trick here is that list comprehension syntax is faster for building the hashmap in python than for loop.

We also have to check if the indices are the same for the two numbers, because we could the same number twice that added up to the target.
