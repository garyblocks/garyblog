## Minimum Window Substring
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Note:**

* If there is no such window in S that covers all characters in T, return the empty string "".
* If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

**Example:**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```
**Code:**

```python
from collections import Counter
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        j = 0
        d = Counter(t)
        required = len(d.keys())
        formed = 0
        min_length = len(s) + 1
        ret = ''
        for i, c in enumerate(s):
            if c not in d:
                continue
            d[c] -= 1
            if d[c] == 0:
                formed += 1 
                
            while j <= i and formed == required:
                if i - j + 1 < min_length:
                    min_length = i - j + 1
                    ret = s[j: i+1]
                if s[j] in d:
                    d[s[j]] += 1
                    if d[s[j]] > 0:
                        formed -= 1
                j += 1 
                
        return ret
```
Keep a dictionary to count the number of characters, when condition is met, move the left pointer until it's not met anymore.
