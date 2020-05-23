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
        hash_map = {}  # use a dictionary because we need to save the index
        for i, n in enumerate(nums):
            # do the check first so we don't use one number twice
            if target - n in hash_map: 
                return [hash_map[target - n], i]
            hash_map[n] = i
```
**Idea:** Use a dictionary to save the numbers we have seen, then we can look up the `target - n` in \\(O(1)\\) time.

**Detail:**

* Create an empty dictionary map the numbers to their index.
* Build the mapping along with the for loop, so we don't have to worry about getting two numbers with the same index, like 3 + 3 = 6.

**Complexity:**

* **Time complexity:** \\(O(n)\\). We traverse the list containing nn elements only once. Each look up in the table costs only \\(O(1)\\) time.

* **Space complexity:** \\(O(n)\\). The extra space required depends on the number of items stored in the hash table, which stores at most n elements.
