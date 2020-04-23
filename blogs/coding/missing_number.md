## Missing Number
Given an array containing n distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example:**

```
Input: [3,0,1]
Output: 2
```
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```
**Note:**
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

**Code:**

```
def missingNumber(self, nums):
    n = len(nums)
    return (n*(n+1)/2) - sum(nums)
```

