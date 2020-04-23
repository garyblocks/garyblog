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

```
import collections
class Solution(object):
    def minWindow(self, s, t):
        if len(s) < len(t):
            return ""
        
        hashmap = collections.Counter(t)
        counter = len(t)
        min_window = ""
        start, end = 0, 0
        
        for end in range(len(s)):
            if hashmap[s[end]] > 0:
                counter -= 1
            hashmap[s[end]] -= 1
            while counter == 0:
                length = end - start + 1
                if not min_window or len(min_window) > length:
                    min_window = s[start:end+1]
                hashmap[s[start]] += 1
                if hashmap[s[start]] > 0:
                    counter += 1
                start += 1
        return min_window
```
