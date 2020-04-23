## Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.

**Example:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Code:**

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        i, j = 0, 0
        max_length = 0
        for j in range(len(s)):
            if s[j] not in s[i:j]:
                max_length = max(j - i + 1, max_length)
            else:
                while s[i] != s[j]:
                    i += 1
                i += 1  # skip the same character
        return max_length
```
Here I used two moving forward pointers, the pointers define the substring we are checking, we loop through the pointer at front, and keep checking the condition, if the condition is not met, we move the pointer at back to next valid position.

Since both pointers will go through the entire array only once, the time complexity O(n).
