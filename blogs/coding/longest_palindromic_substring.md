## Longest Palindromic Substring
Given a string *s*, find the longest palindromic substring in *s*. You may assume that the maximum length of *s* is 1000.

**Example:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
```
Input: "cbbd"
Output: "bb"
```

**Code:**

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        self.max_length, self.ret = 0, ""
        
        def expand(left, right):
            while left > 0 and right < len(s) - 1:
                if s[left-1] == s[right+1]:
                    left -= 1
                    right += 1
                else:
                    break
            if right - left + 1 > self.max_length:
                self.max_length = right - left + 1
                self.ret = s[left: right+1]
        
        for i in range(len(s)):
            expand(i, i)
            if i + 1 < len(s) and s[i] == s[i+1]:
                expand(i, i+1)
        return self.ret
```
Loop through all the numbers and try to expand from the center, check both the single number center and the double numbers center.
