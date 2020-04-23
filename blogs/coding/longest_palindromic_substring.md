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
        max_, ret = 0, ''
        for i in range(len(s)):
            l, d = 1, 0
            while i - d >= 0 and i + d < len(s):
                if s[i-d] == s[i+d]:
                    l = 1 + d * 2
                    if l > max_:
                        max_, ret = l, s[i-d: i+d+1]
                else:
                    break
                d += 1
            if i > 0 and s[i] == s[i-1]:
                l, d = 2, 0
                while i - 1 - d >= 0 and i + d < len(s):
                    if s[i-1-d] == s[i+d]:
                        l = 2 + d * 2
                        if l > max_:
                            max_, ret = l, s[i-1-d: i+d+1]
                    else:
                        break
                    d += 1
        return ret
```
Loop through all the numbers and try to expand, check both single center and double centers.
