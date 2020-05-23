# Longest Substring with At Most Two Distinct Characters

Given a string s , find the length of the longest substring t  that contains at most 2 distinct characters.

**Example:**
```
Input: "eceba"
Output: 3
Explanation: t is "ece" which its length is 3.
```
```
Input: "ccaabbb"
Output: 5
Explanation: t is "aabbb" which its length is 5.
```

**Code:**

```python
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s: str) -> int:
        l = 0
        ret = 0
        max_l = 0
        d = {}
        for r, c in enumerate(s):
            if c in d:
                d[c] += 1
            else:
                while len(d) == 2:
                    d[s[l]] -= 1
                    if not d[s[l]]:
                        d.pop(s[l])
                    l += 1
                d[c] = 1
            max_l = max(max_l, r - l + 1)
        return max_l
```

#### Idea
Two pointers sliding window, use a hashmap to keep the distinct characters count.
